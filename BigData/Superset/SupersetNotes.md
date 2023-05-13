# Notes

- 登录账号/密码：lijzh / li123...



## Remark

- 安装superset

  ```
  教程：https://blog.csdn.net/zgzdqq/article/details/127996901
  教程：https://www.iotword.com/2116.html
  ```

  

- 启动superset

  - 安装 gunicorn  

  ```
  pip install gunicorn -ihttps://pypi.douban.com/simple/
  ```

  - 启动 Superset  

  ```
  gunicorn --workers 5 --timeout 120 --bind l9z102:8787 "superset.app:create_app()" --daemon
  ```

  > 说明：
  >
  > - workers：指定进程个数
  > - timeout： worker 进程超时时间，超时会自动重启
  > - bind：绑定本机地址，即为 Superset 访问地址
  > - daemon：后台运行

  - Web界面：l9z102:8787
  - 停止Superset

  ```
  ps -ef | awk '/superset/ && !/awk/{print $2}' | xargs kill -9
  ```

  > P5 - 05:00 讲解命令

  - 退出环境

  ```
  conda deactivate
  ```

  - superset启停脚本

    > 这里用到的是`python3.9`
  
  ```shell
  #!/bin/bash
  
  superset_status(){
  result=`ps -ef | awk '/gunicorn/ && !/awk/{print $2}' | wc -l`
    if [[ $result -eq 0 ]]; then
      return 0
    else
      return 1
    fi
  }
  
  superset_start(){
    source ~/.bashrc
    superset_status >/dev/null 2>&1
    if [[ $? -eq 0 ]]; then
      conda activate superset3.9; gunicorn --workers 5 --timeout 120 --bind l9z102:8787 --daemon 'superset.app:create_app()'
    else
      echo "superset 正在运行"
    fi
  }
  
  superset_stop(){
    superset_status >/dev/null 2>&1
    if [[ $? -eq 0 ]]; then
      echo "superset 未在运行"
    else
      ps -ef | awk '/gunicorn/ && !/awk/{print $2}' | xargs kill -9
    fi
  }
  
  case $1 in
  start )
    echo "启动 Superset"
    superset_start
  ;;
  stop )
    echo "停止 Superset"
    superset_stop
  ;;
  restart )
    echo "重启 Superset"
    superset_stop
    superset_start
  ;;
  status )
    superset_status >/dev/null 2>&1
    if [[ $? -eq 0 ]]; then
      echo "superset 未在运行"
    else
      echo "superset 正在运行"
    fi
  esac
  ```
  
  