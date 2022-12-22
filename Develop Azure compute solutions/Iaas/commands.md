# CREATE VIRUTAL MACHINE



### CREATE RESOURCE GROUP

1.  USING POWERSHELL

      `New-AzResourceGroup -Name 'myResourceGroup' -Location 'EastUS'`

2.  USING CLI

      `az group create --name myResourceGroup --location eastus`

### CREATE VIRTUAL MACHINE

1.  USING POWERSHELL

      ```
      New-AzVm `
      -ResourceGroupName 'myResourceGroup' `
      -Name 'myVM' `
      -Location 'East US' `
      -VirtualNetworkName 'myVnet' `
      -SubnetName 'mySubnet' `
      -SecurityGroupName 'myNetworkSecurityGroup' `
      -PublicIpAddressName 'myPublicIpAddress' `
      -OpenPorts 80,3389

      ```

2.  USING CLI

    ```
    az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Win2022AzureEditionCore \
    --public-ip-sku Standard \
    --admin-username azureuser 
    ```

### INSTALL WEB SERVER

1.  USING POWERSHELL

      ```
        Invoke-AzVMRunCommand -ResourceGroupName 'myResourceGroup' -VMName 'myVM' -CommandId 'RunPowerShellScript' -ScriptString 
        'Install-WindowsFeature -Name Web-Server -IncludeManagementTools'
      ```

2.  USING CLI

    `az vm run-command invoke -g MyResourceGroup -n MyVm --command-id RunPowerShellScript --scripts "Install-WindowsFeature -name Web-Server -IncludeManagementTools"`
    
    `az vm open-port --port 80 --resource-group myResourceGroup --name myVM`

### CLEAN UP RESOURCES

1.  USING POWERSHELL

      `Remove-AzResourceGroup -Name 'myResourceGroup`

2.  USING CLI

    `az group delete --name myResourceGroup`
