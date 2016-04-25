
## Making a worker

 - `vagrant up` or make a Windows VM
 - `./make_worker.sh` to generate the worker's key
 - Get `/opt/concourse/host_key.pub` from the Concourse VM
 - Add `worker_key.pub` to concourse:

      cd concourse-lite
      vagrant ssh
        cd /opt/concourse
        sudo vi authorized_worker_keys

 - restart Concourse
 - on the Windows VM:

   - install Haskell Platform 7.10.3
   - Download Concourse binary release http://concourse.ci/downloads.html

      .\concourse_windows_amd64.exe worker --work-dir C:\concourse-worker --tsa-host 192.168.100.4 --tsa-public-key .\host_key.pub --tsa-worker-private-key .\worker_key --bind-ip 127.0.0.1 --baggageclaim-bind-ip 127.0.0.1 --tag haskell-7.10.3

 - `fly -t lite workers` to make sure the new worker is registered
