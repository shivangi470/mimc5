# gorth16


it's the example of zkproof
1. to create the pacakge.json file 



    npm init -y

2.Install the Rust 
   
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
    source $HOME/.cargo/env
    

3.Install the circom

     git clone https://github.com/iden3/circom.git
     cd circom
     git checkout master
     cargo build --release
add path=>
     
     
     export PATH=$PATH:$(pwd)/target/release

3. Installing snarkjs,Install snarkjs Globally:


      npm install -g snarkjs
      which snarkjs
      snarkjs --version

  Using snarkjs Locally with npx
        
         npm install snarkjs


4.run file:
     circom circuit.circom --r1cs --wasm
     node ./circuit_js/generate_witness.js ./circuit_js/circuit.wasm ./input.json witness.wtns
     npx snarkjs wtns export json witness.wtns witness.json

5.your changes will be saved in your GitHub repository, and you can continue working from where you left off in your next session

     git status
     git add .
     git commit -m "rust,circom,snarkjs,input.json"
     git push origin main



