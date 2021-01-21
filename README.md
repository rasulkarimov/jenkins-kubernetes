# simple Ci/Cd pipline using Git, Jenkins, Kubernetes
* install and configure kubectl on jenkins server
* sudo permissions required for jenkins user
~~~
echo ‘jenkins ALL=(ALL) NOPASSWD:ALL’ >> /etc/sudoers
~~~
* Job1 
~~~
sudo cp -rfv * /root/DevOpsAL/
~~~

* Job2
~~~
sudo cd /root/DevOpsAL
sudo ls
if sudo kubectl get all|grep webdeploy
then
sudo kubectl delete all —l app=webdeploy
sudo kubectl delete pvc -l app=webdeploy
sudo kubectl apply -f /root/DevOpsAL/webdeploy.yml
sleep 10
sudo kubectl get all
else
sudo kubectl apply -f /root/DevOpsAL/webdeploy.yml
sleep 10
sudo kubectl get all
fi
sudo kubectl cp /root/DevOpsAL/index.html $(sudo kubectl get pod | grep webdeploy | awk '{print$1}'):/var/www/html/index.html
~~~

*
