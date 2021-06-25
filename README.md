# hff-hostpath-provisioner
dynamic hostpath provisioner that support appoint node/path

需求：
1.动态申请hostapth资源：指定storageclass及size
2.storageclass名包括节点名，指定调度到一个节点
3.一个storageclass对应一个节点的路径，可创建多个storageclass对应多个节点的多个路径
