
# singularity container definition for
# Knime hosted on ubuntu 

# Knime download require registration and agreement to to EULA.
# This singularity container is for POC.  
# If you use this, please register your at knime.com

# container size is about 1.8 GB
# Knime workspace will default to $HOME, 
# so that need to be bind mounted to writable location.


#BootStrap: debootstrap
#OSVersion: trusty
#MirrorURL: http://us.archive.ubuntu.com/ubuntu/

BootStrap: docker
From: ubuntu:14.04

%runscript
    echo 'To run Knime from a Singularity container, please start as:  
    echo 'singularity run -B /run tin6150-knime-master.img'
    echo 'Knime Will start momentarily...'
    echo 'Please register at Knime.com when using knime from this Proof of Concept Container. ' 
    sleep 20
    echo ''
    /opt/knime/knime "$@"
    

%post
    echo "Hello from inside the container"
    #sed -i 's/$/ universe/' /etc/apt/sources.list	## dont remember what this was for
    apt-key update
    apt-get update
    apt-get -f -y --force-yes install vim ncurses-term less wget curl tar bzip2 coreutils python zlib1g-dev zlib1g libgtk-3-0 libgtk2.0-0 firefox
    # may actually need nautilus ?  or what's gnome native web browser?  some gtk browser?
    #apt-get -y --force-yes install git
    #apt-get -y --force-yes install gedit			# consistently cause problem :(
    touch /THIS_IS_INSIDE_SINGULARITY
    cd /opt
    # download knime from a temporary location.
    # after POC, need to work out with Greg Landrum et co on way to download from knime.com and get user registration and agreement.
    KNIME_VER=knime_3.4.0
    export KNIME_VER
    KNIME_GZ=${KNIME_VER}.linux.gtk.x86_64.tar.gz 
    export KNIME_GZ
    ##[[ -f $KNIME_GZ ]] || curl https://drive.google.com/file/d/0B1kImCblq9CeRjFranJnV2lCb00/view?usp=sharing -o $KNIME_GZ 
    ##[[ -f $KNIME_GZ ]] || curl https://www.dropbox.com/s/lyzmfu3y6q1x06k/knime_3.4.0.linux.gtk.x86_64.tar.gz?dl=0 -o $KNIME_GZ 
    # http://subdom.ask-margo.com/cache_tmp/knime_3.4.0.linux.gtk.x86_64.tar.gz
    # wget -q to be completely quiet.  hopefully -nv reduces output to sing hub enough.
    test -f $KNIME_GZ || wget --no-verbose https://www.dropbox.com/s/lyzmfu3y6q1x06k/knime_3.4.0.linux.gtk.x86_64.tar.gz?dl=0 -O $KNIME_GZ 
    tar xzf $KNIME_GZ
    rm $KNIME_GZ  # 400 MB for version without "all free extension"
    ln -s $KNIME_VER knime
    echo "Goodbye from inside the container"

