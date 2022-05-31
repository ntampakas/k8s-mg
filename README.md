# zkevm-chain in k8s
## Deploy zkevm-chain + support services to kubernetes cluster

## Deploy EFS storage class, persistent volume claim, and persistent volume
   - Edit pv.yaml and replace volumeHandle with the EFS id retrieved using:
     ```
     aws efs describe-file-systems --query "FileSystems[*].FileSystemId" --output text
     ```
   - Apply configuration
     ```
     kubectl apply -f zkevm-chain/efs
     ```
   - Upload all testnet files to EFS
     F.x.:
     ```
     root@lptp:/home/lptp/repos/k8s-mg# kubectl apply -f zkevm-chain/efs
     root@lptp:/home/lptp/repos/k8s-mg# kubectl apply -f aux/efs-pod.yaml
     root@lptp:/home/lptp/repos/k8s-mg# kubectl get pods
     NAME      READY   STATUS    RESTARTS   AGE
     efs-pod   1/1     Running   0          37s
     root@lptp:/home/lptp/repos/k8s-mg# kubectl cp ~/zkevm-chain/testnet/init.sh efs-pod:/host # etc.
     root@lptp:/home/lptp/repos/k8s-mg# kubectl exec -ti efs-pod -- ls host
     geth.toml                 l1-genesis-template.json  params
     init.sh                   l2-genesis-template.json
     root@lptp:/home/lptp/repos/k8s-mg# kubectl delete -f aux/efs-pod.yaml

     ```

## Deploy zkevm-chain
   ```
   root@lptp:/home/lptp/repos/k8s-mg# kubectl apply -f zkevm-chain/services/
   ```
