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

## Deploy zkevm-chain
   ```
   kubectl apply -f zkevm-chain/services/
   ```
