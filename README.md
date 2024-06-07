# Deploying a Contract on Fuel Network

This tutorial helps to deploy Contract on Fuel Network.
****Note : it is on testnet.***
## Install Dependencies

Update Linux and Install ```curl``` (a command line tool).

```bash
  sudo apt update && sudo apt upgrade -y && sudo apt-get install curl -y
```
![ss1](https://github.com/DanishK023/Fuel-Contracrt-Deployment/assets/108999931/ed4dd4a8-80ae-4f61-aa36-2165b8aace88)

## Install RUST
Installing RUST.  
_*When promt enter ```1```, and hit ```ENTER``` Button._
```bash
  curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
![ss2](https://github.com/DanishK023/Fuel-Contracrt-Deployment/assets/108999931/1eadab4d-2d58-4080-83d9-b5fc8b0dad1e)

Adding RUST to Enviroment, and Checking RUST Version.
```bash
  source $HOME/.cargo/env && rustc --version
```
![ss3](https://github.com/DanishK023/Fuel-Contracrt-Deployment/assets/108999931/1dc97b26-e0d9-4978-91b4-87f7cc6da26d)

## Install git
It will help to Install ```fuelup-init``` script.
```bash
  sudo apt install git -y 
```
![ss4](https://github.com/DanishK023/Fuel-Contracrt-Deployment/assets/108999931/73bfd6ef-4c14-4cc7-b0aa-8f80072c0ed2)

## Install Fuel ToolChain
Installing ```fuelup-init``` script to create contract on Fuel Network.  
enter ```y``` when promt.
```bash
  curl https://install.fuel.network | sh
```
![ss5](https://github.com/DanishK023/Fuel-Contracrt-Deployment/assets/108999931/14d887e7-8a19-4c0b-a6c4-2f9cb4d0f87b)
![ss6](https://github.com/DanishK023/Fuel-Contracrt-Deployment/assets/108999931/570d4006-cf09-4e11-a7ed-e90e882b8b29)  
>Adding PATH to system
  ```bash
    source /root/.bashrc
  ```

# Set-Up Your Fuel Wallet

THERE IS TWO STEPS ```CREATE NEW WALLET``` & ```IMPORTING OLD WALLET```

>**CREATE NEW WALLET**
Initialize a new wallet
```bash
  forc wallet new
```
Enter a password(Note : it will not vicible when you entering), and be sure to save the mnemonic phrase that is output.  

![wall2](https://github.com/DanishK023/Fuel-Contracrt-Deployment/assets/108999931/bc8962ab-29ca-4b03-9a36-496bdf2d8d61)

![wall1](https://github.com/DanishK023/Fuel-Contracrt-Deployment/assets/108999931/9fd80417-0ffc-4162-bc0d-4bfbb2aab36d)

Next, create a new wallet account with
```bash
  forc wallet account new
```
*_Enter Password. It will show Your Fuel Address._   
![IMG_20240608_010748](https://github.com/DanishK023/Fuel-Contracrt-Deployment/assets/108999931/921e3014-e33e-4d84-be54-171b70c3fea8)

>**IMPORTING OLD WALLET**
If You Have OLD Wallet You Can Import it BY:
```bash
  forc wallet import 
```
_When Prompt Enter you mnemonic phrase and Password._  
![wall4](https://github.com/DanishK023/Fuel-Contracrt-Deployment/assets/108999931/b4f828bb-e634-4b15-b225-2d2686d8b0e4)  
Add new wallet account with
```bash
  forc wallet account new
```
*_Enter Password. It will show Your Fuel Address._  

![IMG_20240608_010748](https://github.com/DanishK023/Fuel-Contracrt-Deployment/assets/108999931/12bab655-ac84-4110-a819-9d3e4ef03835)


If You Need To Check You account
```bash
  forc wallet accounts 
```

****You Need GAS FEES.****  
Go to [faucet](https://faucet-testnet.fuel.network/)
Enter Your ```Wallet Address```

## Create Project and Contract.
Creating Project with ```My-Project``` name.  
_*you can choose name of your project, simply change ```My-Project``` from command._
```bash
  mkdir My-Project && cd My-Project
```
![ss7](https://github.com/DanishK023/Fuel-Contracrt-Deployment/assets/108999931/28a88612-1b6b-4001-bfbe-0f1a2119f0e7)

Now Run Command to Create Contract.
```bash
  forc new counter-contract
```
![ss8](https://github.com/DanishK023/Fuel-Contracrt-Deployment/assets/108999931/cc5cde24-1ec1-40c0-9362-a2a82241653d)

## Editing the Contract File.
Editing ```main.sw``` file.
```bash
  nano counter-contract/src/main.sw
```
![ss9](https://github.com/DanishK023/Fuel-Contracrt-Deployment/assets/108999931/995a1f05-b7ec-492a-b7e3-1324e531a2b8)

***DELETE EVERYTHING*** and Copy Below ```Code``` and Paste.
```bash
  contract;
 
storage {
    counter: u64 = 0,
}
 
abi Counter {
    #[storage(read, write)]
    fn increment();
 
    #[storage(read)]
    fn count() -> u64;
}
 
impl Counter for Contract {
    #[storage(read)]
    fn count() -> u64 {
        storage.counter.read()
    }
 
    #[storage(read, write)]
    fn increment() {
        let incremented = storage.counter.read() + 1;
        storage.counter.write(incremented);
    }
}
```
![ss10](https://github.com/DanishK023/Fuel-Contracrt-Deployment/assets/108999931/4eb34589-66f6-4347-b349-6c875ed2dd71)

After Pasting, Press ```CTRL+X``` enter ```y``` and Press ```ENTER``` Button.

# Build Contract

Move to ```counter-contract``` Directory.
```bash
  cd counter-contract
```
Next, run the forc build command
```bash
  forc build 
```
![ss11](https://github.com/DanishK023/Fuel-Contracrt-Deployment/assets/108999931/41a473ed-e5b3-487e-a997-e9f65b1c48eb)


# Deploying Contract (Last STEP)

Deploy Your Contract.
```bash
  forc deploy --testnet
```
Eneter Your ```Password```, then Enter ```0``` , and enter ```y```    

![photo_2024-06-08_01-12-59](https://github.com/DanishK023/Fuel-Contracrt-Deployment/assets/108999931/bd569b65-cc5e-437f-b3da-76bd093cadf9)  

# Voila! Your Contract Created.
## Check On Fuel Explorer.
Enter You Contract ID [here](https://app.fuel.network/)

