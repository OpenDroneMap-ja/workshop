# OpenDroneMap_Workshop - How to "OpenDroneMap"
仮想環境に6GB割り当ててます。その負荷に耐えられるPCを準備してください。


##Vagrantの準備

###①Vagrant Boxの準備

```bash
$ vagrant plugin install vagrant-vbguest
$ vagrant box add ubuntu14_04_64 https://github.com/kraksoft/vagrant-box-ubuntu/releases/download/14.04/ubuntu-14.04-amd64.box
$ mkdir odm_JapanPack
$ cd odm_JapanPack/
$ vagrant init ubuntu14_04_64 
```

###②Vagrantfileの編集

メモリとネットワークの共有を設定

```ruby
$ vi Vagrantfile
# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu14_04_64"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
   config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
   config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
   config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
     vb.memory = "6144"
   end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  # config.vm.provision "shell", inline: <<-SHELL
  #   sudo apt-get update
  #   sudo apt-get install -y apache2
  # SHELL
end 

```

## 以下の仮想環境立ち上げコマンドを実行

$ vagrant up

$ vagrant ssh

##OpenDroneMapのインストール

###①ソースコードをGitHubよりClone

```bash
$ sudo apt-get update
$ sudo apt-get install git-core
$ cd /vagrant
$ git clone https://github.com/OpenDroneMap/OpenDroneMap.git
```

###②OpenDroneMapをインストール

```bash
$ cd OpenDroneMap/
$ ./install.sh
	
	     created by Daniel Schwarz/daniel.schwarz@topoi.org
	     released under Creative Commons/CC-BY
	     Attribution
	
	     if the script doesn't finish properly
	     (i.e. it doesn't print "script finished" at the end)
	     please email me the content of the logs folder
	
	
	  - script started - Tue Mar  8 03:23:20 GMT 2016
	
	  > installing required packages
	    - updating
	    - installing
	Downloading/unpacking networkx
	  Downloading networkx-1.11-py2.py3-none-any.whl (1.3MB): 1.3MB downloaded
	Downloading/unpacking exifread
	  Downloading ExifRead-2.1.2-py2-none-any.whl (47kB): 47kB downloaded
	Downloading/unpacking xmltodict
	  Downloading xmltodict-0.10.1.tar.gz
	  Running setup.py (path:/tmp/pip_build_root/xmltodict/setup.py) egg_info for package xmltodict
	    
	Requirement already satisfied (use --upgrade to upgrade): decorator>=3.4.0 in /usr/lib/python2.7/dist-packages (from networkx)
	Installing collected packages: networkx, exifread, xmltodict
	  Running setup.py install for xmltodict
	    
	Successfully installed networkx exifread xmltodict
	Cleaning up...
	    - installing git submodules
	Submodule 'src/bundler' (https://github.com/chris-cooper/bundler_sfm) registered for path 'src/bundler'
	Cloning into 'src/bundler'...
	remote: Counting objects: 1394, done.
	remote: Total 1394 (delta 0), reused 0 (delta 0), pack-reused 1394
	Receiving objects: 100% (1394/1394), 6.02 MiB | 1.00 MiB/s, done.
	Resolving deltas: 100% (443/443), done.
	Checking connectivity... done.
	Submodule path 'src/bundler': checked out 'b34cc5dcd54345272028b68f82fa4d0ae8a103c9'
	  < done - Tue Mar  8 03:30:03 GMT 2016
	
	  > getting the sources
	    - getting http://ftp.gnu.org/gnu/parallel/parallel-20141022.tar.bz2
	######################################################################## 100.0%
	    - finished parallel.tar.bz2
	
	    - already downloaded http://www.netlib.org/clapack/clapack-3.2.1-CMAKE.tgz
	    - already downloaded http://www.cs.jhu.edu/~misha/Code/PoissonRecon/Version2/PoissonRecon.zip
	    - already downloaded http://www.vlfeat.org/download/vlfeat-0.9.13-bin.tar.gz
	    - already downloaded http://www.di.ens.fr/cmvs/cmvs-fix2.tar.gz
	    - already downloaded http://smathermather.github.io/BundlerTools/patched_files/src/graclus/graclus1.2.tar.gz
	    - getting https://github.com/PointCloudLibrary/pcl/archive/pcl-1.7.2.tar.gz
	######################################################################## 100.0%
	    - finished pcl.tar.gz
	
	    - getting http://ceres-solver.org/ceres-solver-1.10.0.tar.gz
	######################################################################## 100.0%
	    - finished ceres-solver.tar.gz
	
	    - getting http://lastools.org/download/LAStools.zip
	######################################################################## 100.0%
	    - finished LAStools.zip
	
	Cloning into '/vagrant/OpenDroneMap/src/opengv'...
	remote: Counting objects: 6491, done.
	remote: Total 6491 (delta 0), reused 0 (delta 0), pack-reused 6491
	Receiving objects: 100% (6491/6491), 6.56 MiB | 855.00 KiB/s, done.
	Resolving deltas: 100% (3422/3422), done.
	Checking connectivity... done.
	Checking out files: 100% (4357/4357), done.
	Cloning into '/vagrant/OpenDroneMap/src/OpenSfM'...
	remote: Counting objects: 5380, done.
	remote: Total 5380 (delta 0), reused 0 (delta 0), pack-reused 5380
	Receiving objects: 100% (5380/5380), 18.58 MiB | 2.84 MiB/s, done.
	Resolving deltas: 100% (3534/3534), done.
	Checking connectivity... done.
	  < done - Tue Mar  8 03:32:31 GMT 2016
	
	  - unzipping sources
	  < done - Tue Mar  8 03:32:45 GMT 2016
	
	  - copying patches
	
	  < done - Tue Mar  8 03:32:45 GMT 2016
	
	  - building
	
	  > graclus
	    - cleaning graclus
	    - building graclus
	  < done - Tue Mar  8 03:32:58 GMT 2016
	
	  > poisson surface reconstruction 
	    - building poisson surface reconstruction
	  < done - Tue Mar  8 03:33:03 GMT 2016
	
	  > parallel
	    - configuring parallel
	    - building paralel
	  < done - Tue Mar  8 03:33:04 GMT 2016
	
	  > clapack
	    - building clapack
	    - installing clapack
	  < done - Tue Mar  8 03:37:43 GMT 2016
	
	  > vlfeat
	    - installing vlfeat
	  < done - Tue Mar  8 03:37:43 GMT 2016
	
	  > LAStools
	    - installing LAStools
	  < done - Tue Mar  8 03:38:10 GMT 2016
	
	  > cmvs/pmvs
	    - cleaning cmvs
	    - building cmvs
	    - make depend cmvs
	  < done - Tue Mar  8 03:38:31 GMT 2016
	
	  > ceres
	    - configuring ceres
	    - building ceres
	  < done - Tue Mar  8 03:41:55 GMT 2016
	
	  > bundler
	    - cleaning bundler
	    - building bundler
	  < done - Tue Mar  8 03:42:42 GMT 2016
	
	  > pcl 
	    - configuring pcl
	    - building and installing pcl
	  < done - Tue Mar  8 03:51:05 GMT 2016
	
	  > meshing 
	    - configuring odm_meshing
	    - building odm_meshing
	  < done - Tue Mar  8 03:51:24 GMT 2016
	
	  > texturing 
	    - configuring odm_texturing
	    - building odm_texturing
	  < done - Tue Mar  8 03:51:52 GMT 2016
	
	  > extract_utm 
	    - configuring odm_extract_utm
	    - building odm_extract_utm
	  < done - Tue Mar  8 03:51:54 GMT 2016
	
	  > georef 
	    - configuring odm_georef
	    - building odm_georef
	  < done - Tue Mar  8 03:52:17 GMT 2016
	
	  > orthophoto 
	    - configuring odm_orthophoto
	    - building odm_orthophoto
	  < done - Tue Mar  8 03:52:33 GMT 2016
	
	  > OpenGV
	    - configuring opengv
	Branch python-wrapper set up to track remote branch python-wrapper from origin.
	Switched to a new branch 'python-wrapper'
	    - building opengv
	  < done - Tue Mar  8 03:58:16 GMT 2016
	
	  > OpenSfM
	    - configuring opensfm
	Note: checking out 'odm-2'.
	
	You are in 'detached HEAD' state. You can look around, make experimental
	changes and commit them, and you can discard any commits you make in this
	state without impacting any branches by performing another checkout.
	
	If you want to create a new branch to retain commits you create, you may
	do so (now or later) by using -b with the checkout command again. Example:
	
	  git checkout -b new_branch_name
	
	HEAD is now at a0671c4... Ignore matching_gps_neighbors if any image has no GPS data
	    - building opensfm
	  < done - Tue Mar  8 03:58:48 GMT 2016
	
	  - script finished - Tue Mar  8 03:58:52 GMT 2016
```

###③OpenDroneMapのコマンド確認

`./run.py -h`が立ち上がれば起動完了

```bash
$ ./run.py -h
	usage: run.py [-h] [--resize-to <integer>] [--job-dir-name <string>]
	              [--start-with <task>] [--end-with <task>] [--run-only <task>]
	              [--use-opensfm | --use-bundler] [--force-focal <positive float>]
	              [--force-ccd <positive float>] [--min-num-features <integer>]
	              [--matcher-threshold <percent>] [--matcher-ratio <float>]
	              [--matcher-neighbors <integer>] [--matcher-distance <integer>]
	              [--cmvs-maxImages <integer>] [--pmvs-level <positive integer>]
	              [--pmvs-csize < positive integer>]
	              [--pmvs-threshold <float: -1.0 <= x <= 1.0>]
	              [--pmvs-wsize <positive integer>]
	              [--pmvs-minImageNum <positive integer>]
	              [--odm_meshing-maxVertexCount <positive integer>]
	              [--odm_meshing-octreeDepth <positive integer>]
	              [--odm_meshing-samplesPerNode <float >= 1.0>]
	              [--odm_meshing-solverDivide <positive integer>]
	              [--odm_texturing-textureResolution <positive integer>]
	              [--odm_texturing-textureWithSize <positive integer>]
	              [--odm_georeferencing-gcpFile <path string>]
	              [--odm_georeferencing-useGcp]
	              [--odm_orthophoto-resolution <float > 0.0>] [--zip-results]
	
	OpenDroneMap
	
	optional arguments:
	  -h, --help            show this help message and exit
	  --resize-to <integer>
	                        Resizes images by the largest side. Default: 2400
	  --job-dir-name <string>
	                        Name of the output folder, only ASCII charaters can be
	                        used. If not provided "reconstruction-with-image-size
	                        -[resize-to]" will be used
	  --start-with <task>, -s <task>
	                        Start with the provided task. Can be one of: resize |
	                        opensfm | getKeypoints | match | bundler | cmvs | pmvs
	                        | odm_meshing | odm_texturing | odm_georeferencing |
	                        odm_orthophoto
	  --end-with <task>, -e <task>
	                        Finish at the provided task. Can be one of: resize |
	                        opensfm | getKeypoints | match | bundler | cmvs | pmvs
	                        | odm_meshing | odm_texturing | odm_georeferencing |
	                        odm_orthophoto
	  --run-only <task>     Run only one task. Can be one of: resize | opensfm |
	                        getKeypoints | match | bundler | cmvs | pmvs |
	                        odm_meshing | odm_texturing | odm_georeferencing |
	                        odm_orthophoto
	  --use-opensfm         use OpenSfM to find the camera positions (replaces
	                        getKeypoints, match and bundler steps)
	  --use-bundler         use Bundler to find the camera positions.
	  --force-focal <positive float>
	                        Override the focal length information for the images
	  --force-ccd <positive float>
	                        Override the ccd width information for the images
	  --min-num-features <integer>
	                        Minimum number of features to extract per image. More
	                        features leads to better results but slower execution.
	                        Default: 6000
	  --matcher-threshold <percent>
	                        Ignore matched keypoints if the two images share less
	                        than <float> percent of keypoints. Default: 2.0
	  --matcher-ratio <float>
	                        Ratio of the distance to the next best matched
	                        keypoint. Default: 0.6
	  --matcher-neighbors <integer>
	                        Number of nearest images to pre-match based on GPS
	                        exif data. Set to 0 to skip pre-matching. Neighbors
	                        works together with Distance parameter, set both to 0
	                        to not use pre-matching. OpenSFM uses both parameters
	                        at the same time, Bundler uses only one which has
	                        value, prefering the Neighbors parameter. Default: 8
	  --matcher-distance <integer>
	                        Distance threshold in meters to find pre-matching
	                        images based on GPS exif data. Set to 0 to skip pre-
	                        matching. Default: 0
	  --cmvs-maxImages <integer>
	                        The maximum number of images per cluster. Default: 500
	  --pmvs-level <positive integer>
	                        The level in the image pyramid that is used for the
	                        computation. see
	                        http://www.di.ens.fr/pmvs/documentation.html for more
	                        pmvs documentation. Default: 1
	  --pmvs-csize < positive integer>
	                        Cell size controls the density of reconstructions.
	                        Default: 2
	  --pmvs-threshold <float: -1.0 <= x <= 1.0>
	                        A patch reconstruction is accepted as a success and
	                        kept, if its associcated photometric consistency
	                        measure is above this threshold. Default: 0.7
	  --pmvs-wsize <positive integer>
	                        pmvs samples wsize x wsize pixel colors from each
	                        image to compute photometric consistency score. For
	                        example, when wsize=7, 7x7=49 pixel colors are sampled
	                        in each image. Increasing the value leads to more
	                        stable reconstructions, but the program becomes
	                        slower. Default: 7
	  --pmvs-minImageNum <positive integer>
	                        Each 3D point must be visible in at least minImageNum
	                        images for being reconstructed. 3 is suggested in
	                        general.
	  --odm_meshing-maxVertexCount <positive integer>
	                        The maximum vertex count of the output mesh. Default:
	                        100000
	  --odm_meshing-octreeDepth <positive integer>
	                        Oct-tree depth used in the mesh reconstruction,
	                        increase to get more vertices, recommended values are
	                        8-12, the default is 9
	  --odm_meshing-samplesPerNode <float >= 1.0>
	                        Number of points per octree node, recommended and
	                        default value: 1.0
	  --odm_meshing-solverDivide <positive integer>
	                        Oct-tree depth at which the Laplacian equation is
	                        solved in the surface reconstruction step. Increasing
	                        this value increases computation times slightly but
	                        helps reduce memory usage. Default: 9
	  --odm_texturing-textureResolution <positive integer>
	                        The resolution of the output textures. Must be greater
	                        than textureWithSize. Default: 4096
	  --odm_texturing-textureWithSize <positive integer>
	                        The resolution to rescale the images performing the
	                        texturing. Default: 3600
	  --odm_georeferencing-gcpFile <path string>
	                        path to the file containing the ground control points
	                        used for georeferencing. The default file is
	                        gcp_list.txt. The file needs to be on the following
	                        line format: easting northing height pixelrow pixelcol
	                        imagename
	  --odm_georeferencing-useGcp
	                        Enabling GCPs from the file above. The GCP file is not
	                        used by default.
	  --odm_orthophoto-resolution <float > 0.0>
	                        Orthophoto ground resolution in pixels/meter. Default:
	                        20.0
	  --zip-results         Compress the results using gunzip


```


##OpenDroneMapを用いた空撮画像の処理
###処理手順（サンプル・データ）
①空撮画像のフォルダに移動

```bash
$ cd /vagrant/odm_data
$ ls
	apt  benchmark  caliterra  keioSFC  langley  pacifica  README.md  seneca  snowpeak
```
②benchmarkでの空撮画像処理テスト

```bash
$ cd benchmark/
$ ls
	DSC05507.JPG  DSC05511.JPG  DSC05515.JPG  DSC05519.JPG  DSC05523.JPG  DSC05527.JPG  DSC05531.JPG
	DSC05508.JPG  DSC05512.JPG  DSC05516.JPG  DSC05520.JPG  DSC05524.JPG  DSC05528.JPG  README.md
	DSC05509.JPG  DSC05513.JPG  DSC05517.JPG  DSC05521.JPG  DSC05525.JPG  DSC05529.JPG
	DSC05510.JPG  DSC05514.JPG  DSC05518.JPG  DSC05522.JPG  DSC05526.JPG  DSC05530.JPG
$ ./../../OpenDroneMap/run.py
```
以下のフォルダができていれば正常に動作  
`reconstruction-with-image-size-2400`  
`reconstruction-with-image-size-2400-results`

③caliterraの空撮画像を用いた処理

```bash
$ cd /vagrant/odm_data/
$ git clone https://github.com/OpenDroneMap-ja/odm_data_caliterra.git
$ cd odm_data_caliterra
$ ./../../OpenDroneMap/run.py
$ cd reconstruction-with-image-size-2400-results

```
完成イメージ

![odm_orthphoto_caliterra.png](https://raw.githubusercontent.com/Kenyat1989/Markdown/710e53411357261f8e89496bd58cff85daf81902/image/odm_orthphoto_caliterra_resize.png?token=AHBEx59qM4qNMxoq4PvcKI0vqEayYmxyks5W8kqEwA%3D%3D)

④senecaの空撮画像を用いた処理

```bash
$ cd /vagrant/odm_data/
$ git clone https://github.com/OpenDroneMap-ja/odm_data_seneca.git
$ cd odm_data_seneca
$ ./../../OpenDroneMap/run.py
$ cd reconstruction-with-image-size-2400-results

```
完成イメージ

![odm_orthphoto_seneca.png](https://raw.githubusercontent.com/Kenyat1989/Markdown/710e53411357261f8e89496bd58cff85daf81902/image/odm_orthphoto_seneca_resize.png?token=AHBEx-xBdQnnahxKLk_1Vfw3VVg_2SFxks5W8ktfwA%3D%3D)

###OpenDroneMapの出力結果
OpenDronMapの処理をすると2つのサブフォルダが作成されます。フォルダ名はデフォルトで`reconstruction-with-image-size-[resize-to]`と出力されますが、 `--job-dir-name`のオプションを用いると出力フォルダ名を変更することができます。

**フォルダ詳細**

- `{job-dir-name} (eg.:reconstruction-with-image-size-2400) `-- 実行結果や一時ファイルなどが出力されます (resized images, logs, temp files, etc...)

- `{job-dir-name}-results (eg.:reconstruction-with-image-size-2400-results)` -- 画像処理したコンテンツが出力されます ( point cloud, fully textured meshes, orthophoto, etc..)

###出力されるコンテンツの種類
**Meshing**

- `option-0000.ply` -- ポイントクラウドデータ（3Dモデル）
- `odm_mesh-0000.ply` -- メッシュサーフェスデータ（面データ）

**Texturing**

- `odm_texturing/odm_textured_model.obj` -- テキスチャ付きメッシュサーフェスデータ
- `reconstruction-with-image-size-1200-results\odm_texturing\odm_textured_model.obj`からMeshLabにて読み込むことができます。

**Georeferencing**

- `odm_texturing/odm_textured_model_geo.obj` -- 地理情報とテキスチャを付与したメッシュサーフェスデータ
- `option-0000_georef.ply` -- 地理情報付きポイントクラウドクラウドデータ（3Dモデル）
- `odm_textured_model_geo_georef_system.txt` -- X,Y座標の書かれたテキストデータ
- `pointcloud_georef.laz` -- LAZ file

**Orthophoto**

- `odm_orthphoto.png` -- PNG形式のオルソ化空撮画像ですが、地理情報は付加されていません。
- `odm_orthphoto.tif` -- GeoTIFF形式のオルソ化空撮画像です。GISソフトウェアのラスタレイヤとして利用できます。

##OpenDroneMapの日本版パッケージ作成（Vagrant boxの作成）

###①Vagrant Box作成
```bash
$ vagrant halt #vagrantを停止する
$ vagrant package
	==> box: Box file was not detected as metadata. Adding it directly...
	==> box: Adding box 'odm_package' (v0) for provider: 
	    box: Unpacking necessary files from: file:///Users/kenyat/vagrant/odm_JapanPack/package.box
	==> box: Successfully added box 'odm_package' (v0) for 'virtualbox'!
$ ls
	OpenDroneMap  Vagrantfile  odm_data  package.box
```

###②Vagrant fileの書き直し
変更点： `config.vm.box = "odm_package"`

```bash
$ vi Vagrantfile
	# -*- mode: ruby -*-
	# vi: set ft=ruby :
	
	# All Vagrant configuration is done below. The "2" in Vagrant.configure
	# configures the configuration version (we support older styles for
	# backwards compatibility). Please don't change it unless you know what
	# you're doing.
	Vagrant.configure(2) do |config|
	  # The most common configuration options are documented and commented below.
	  # For a complete reference, please see the online documentation at
	  # https://docs.vagrantup.com.
	
	  # Every Vagrant development environment requires a box. You can search for
	  # boxes at https://atlas.hashicorp.com/search.
	  config.vm.box = "odm_package"
	
	  # Disable automatic box update checking. If you disable this, then
	  # boxes will only be checked for updates when the user runs
	  # `vagrant box outdated`. This is not recommended.
	  # config.vm.box_check_update = false
	
	  # Create a forwarded port mapping which allows access to a specific port
	  # within the machine from a port on the host machine. In the example below,
	  # accessing "localhost:8080" will access port 80 on the guest machine.
	   config.vm.network "forwarded_port", guest: 80, host: 8080
	
	  # Create a private network, which allows host-only access to the machine
	  # using a specific IP.
	   config.vm.network "private_network", ip: "192.168.33.10"
	
	  # Create a public network, which generally matched to bridged network.
	  # Bridged networks make the machine appear as another physical device on
	  # your network.
	  # config.vm.network "public_network"
	
	  # Share an additional folder to the guest VM. The first argument is
	  # the path on the host to the actual folder. The second argument is
	  # the path on the guest to mount the folder. And the optional third
	  # argument is a set of non-required options.
	  # config.vm.synced_folder "../data", "/vagrant_data"
	
	  # Provider-specific configuration so you can fine-tune various
	  # backing providers for Vagrant. These expose provider-specific options.
	  # Example for VirtualBox:
	  #
	   config.vm.provider "virtualbox" do |vb|
	  #   # Display the VirtualBox GUI when booting the machine
	  #   vb.gui = true
	  #
	  #   # Customize the amount of memory on the VM:
	     vb.memory = "6144"
	   end
	  #
	  # View the documentation for the provider you are using for more
	  # information on available options.
	
	  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
	  # such as FTP and Heroku are also available. See the documentation at
	  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
	  # config.push.define "atlas" do |push|
	  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
	  # end
	
	  # Enable provisioning with a shell script. Additional provisioners such as
	  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
	  # documentation for more information about their specific syntax and use.
	  # config.vm.provision "shell", inline: <<-SHELL
	  #   sudo apt-get update
	  #   sudo apt-get install -y apache2
	  # SHELL
	end

```

##OpenDroneMap日本版パッケージの使い方
###①Vagrantの設定と立ち上げ
```bash
$ vagrant plugin install vagrant-vbguest
$ vagrant box add odm_package package.box
$ vagrant up
$ vagrant ssh
```

###②OpenDroneMapの動作テスト
```bash
$ cd /vagrant/OpenDroneMap/
$ ./run.py -h
#ここで起動すれば問題なくOpenDroneMapの処理を実行できます
```

###③サンプル・データにアクセスし、処理の実行
```bash
$ cd /vagrant/odm_data/　　#以下のディレクトリにサンプル・データがあります
$ ls
	apt  benchmark  caliterra  keioSFC  langley  pacifica  README.md  seneca  snowpeak
$ cd {data_name/}
$ ./../../OpenDroneMap/run.py
```

##OpenDroneMapのサンプル・データ一覧
OpenDroneMapを用いるためのサンプル・データ集です。  
初心者の方は太字に示されているデータから扱うことをオススメします

リポジトリ名 | 画像数 | サイズ (MB) | Coordinates in EXIF: | GCPs in File:
------|:----------:|:-----------:|:----------------------:|:---------------:
odm_data_apt | 76 | 579 | ✕ | ✕
odm_data_benchmark | 25 | 106 | ◯ | ✕
**odm_data_caliterra** | 77 | 272 | ◯ | ✕
odm_data_langley | 200 | 706 | ✕ | ✕
odm_data_pacifica | 12 | 66.4 | ✕ | ✕
odm_data_seneca | 167 | 358 | ◯ | ✕
odm_data_keioSFC | 194 | 979.7 |  ◯ | ✕
odm_data_snowpeak | 140 | 767.3 |  ◯ | ✕

