dynamic hostpath provisioner that support appoint node/path

# 需求： 
1.动态申请hostapth资源：指定storageclass及size 
2.storageclass名包括节点名
3.一个storageclass对应一个节点的路径，可创建多个storageclass对应多个节点的多个路径

# 编译：
你可以修改镜像名和版本号
make

# 部署：
1. 上传镜像
2. kubectl apply -f hostpath-provisioner.yaml

# 使用：
1. 创建storageclass指定节点及路径(storageclass:hostpath-node1-ssd 对应node1的/var/hostpath/ssd路径)
'''
#kubectl apply -f sc.yaml
kind: StorageClass
apiVersion: storage.k8s.io/v1beta1
metadata:
  name: hostpath-node1-ssd
provisioner: hff.io/hostpath
parameters:
  hostPathName: ssd
'''

2. 节点打上标签
kubectl annotate node node1 hostpath.hff.io/ssd=/var/hostpath/ssd

3. 创建pvc
'''
#kubectl apply -f pvc.yaml
kind: PersistentVolumeClaim
apiVersion: v1
metadata:
  name: test-pvc
spec:
  storageClassName: hostpath-node1-ssd
  accessModes:
    - ReadWriteMany
  resources:
    requests:
      storage: 1Gi
'''