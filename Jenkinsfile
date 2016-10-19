stage 'pre-checks'
node('gljumper') {
   echo "Retrieve builds from gljumper"
   sh 'hostname'
   sh 'uname -a'
      
}

stage 'Installer build'
echo "Getting build images"

parallel 'getting image for win64': {
     node { build 'Installer/GetBuildImage_win64' }
}, 
'Getting image for freebsd': {
     node { build 'Installer/GetBuildImage_freebsd64' }
},
'Getting image for linux': {
     node { build 'Installer/GetBuildImage_freebsd64' }
}


//build 'Installer/GetBuildImage_win64'
//build 'Installer/GetBuildImage_freebsd64'
//build 'Installer/GetBuildImage_linux64'
node 
{
   build 'Installer/FTPImagesToInstaller'
}

stage 'Installer extract images'
parallel 'Extract windows': {
    node { build 'Installer/ExtractImage_win64' }
},
'Extract freebsd': {
    node { build 'Installer/ExtractImage_freebsd64' }
},
'Extract linux': {
    node { build 'Installer/ExtractImage_linux64' }
}

//build 'Installer/FTPImagesToInstaller'
//build 'Installer/ExtractImage_win64'
//build 'Installer/ExtractImage_linux64'
//build 'Installer/ExtractImage_freebsd64'

stage 'Installer run'
node ('installer')
{
   echo 'On windows'
   bat 'hostname'
   
}

stage 'Installer copy to test servers'
node {
    echo "Hello from testing stage"
    sh 'hostname'
}