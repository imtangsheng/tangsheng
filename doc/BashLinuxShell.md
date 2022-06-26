[Shell(Bash)脚本教程](https://www.runoob.com/linux/linux-shell.html)

第一个shell脚本

test.sh:

    #!/bin/bash
    echo "Hello World !"

运行实例 »

    chmod +x ./test.sh  #使脚本具有执行权限
    ./test.sh  #执行脚本

作为解释器参数

    /bin/sh test.sh
    // 或
    bash test.sh
