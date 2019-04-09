init_physical_machine.sh
├── k8s-dashboard
│   ├── 01_pull_dashboard_image.sh
│   ├── 02_create_dashboard.sh
│   ├── 02_delete_dashboard.sh
│   ├── 03_check_dashboard.sh
│   └── dashboard
│       ├── heapster
│       │   ├── grafana.yaml
│       │   ├── heapster.yaml
│       │   └── influxdb.yaml
│       ├── kubernetes-dashboard-admin.rbac.yaml
│       └── kubernetes-dashboard.yaml
├── k8s-v1.11.2
│   ├── 01_replace_centos_yum_aliyun.sh
│   ├── 02_check_and_configure_environment.sh
│   ├── 03_install_docker.sh
│   ├── 04_install_kubernetes.sh
│   ├── 05_pull_kubernetes_image_from_aliyun.sh
│   ├── 05_pull_kubernetes_image_slave_from_aliyun.sh
│   ├── 06_kubeadm_init_on_master.sh
│   ├── aliyum
│   │   ├── CentOS-Base.repo
│   │   ├── epel.repo
│   │   ├── RPM-GPG-KEY-CentOS-7
│   │   └── RPM-GPG-KEY-CentOS-7-aarch64
│   ├── kubernetes
│   │   ├── cni-plugins-arm64-v0.7.1.tgz
│   │   └── kubernetes.repo
│   ├── log
│   │   └── kubeadm-init.txt
│   ├── master_install_k8s_v1.11.2.sh
│   ├── Readme.txt
│   └── slave_install_k8s_v1.11.2.sh
└── Readme.txt

此脚本用于centos-7-aarch64安装kuberneters软件！！

################################################ step 1 ###################################
init_physical_machine.sh [hostname] [static IP]

设置服务器的主机名和静态IP

################################################ step 2 ###################################
k8s-v1.11.2

安装kuberneters-v1.11.2

（1）01_replace_centos_yum_aliyun.sh
     更换CentOS的YUM源为阿里源！

（2）02_check_and_configure_environment.sh
     对系统做kuberneters初始化操作，包括NTP时间同步、关闭防火墙、关闭swap、关闭SELinux等

（3）03_install_docker.sh
     安装docker-18.06

（4）04_install_kubernetes.sh
     安装kuberneters-v1.11.2

（5）05_pull_kubernetes_image_from_aliyun.sh
     在master上执行，pull取kuberneters初始化所需的镜像
     05_pull_kubernetes_image_slave_from_aliyun.sh
     在nodes上执行，pull取kuberneters nodes节点所需的镜像

（6）06_kubeadm_init_on_master.sh
     在master上执行，初始化kuberneters集群

（7）将nodes节点加入到k8s集群中，参看06_kubeadm_init_on_master.sh输出的信息，存在./log/kubeadm-init.txt中

################################################ step 3 ###################################
k8s-dashboard 

安装图型化监控界面

（1）01_pull_dashboard_image.sh
     拉取dashboard所需的依赖docker镜像

（2）02_create_dashboard.sh
     启动dashboard所需的所有yaml文件

     02_delete_dashboard.sh
     停止所有的dashboard的所有镜像

（3）03_check_dashboard.sh
     查看dashboad的相关镜像是否启动成功

