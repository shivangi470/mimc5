# mimc5



MIMC is a block cipher and hash function family designed specifically for SNARK applications. The low multiplicative complexity of MiMC over prime fields makes it suitable for ZK-SNARK applications such as ZCash.

The key scheduling adds the same (uniformly randomly chosen secret) key k ∈ Fq at each round and is followed by the round constant addition. In detail, the encryption function of MiMC is Ex(x)=(Fr1 Fr-2 Fo)(x) + k,

where x ∈ IFq is the plaintext, r is the number of rounds, F, is the round function for round i ≥ 0, and ke Fo is the key. Each F, is defined as Fi(x) = (x + k + c)³, where qe Fq are the round constants and Co = 0. The round constants are chosen as random elements of Fq at the instantiation of MiMC and then fixed. Note that there are no round keys, instead the same key is used in each round and once at the end. All the operations are defined in the underlying field Fq.

![WhatsApp Image 2024-07-18 at 11 37 12_02b35648](https://github.com/user-attachments/assets/e884072e-2279-4e85-941d-308053b7000c)





MiMC Encryption Flow
Initialization

    Input:
        Plaintext x∈Fq​ (where Fq​ is a finite field with prime order q).
        Secret key k∈Fq​.
        Number of rounds r.
        Round constants ci​∈Fq​ for i=0,1,…,r−1, where c0=0.

Encryption Process

    Initial State:
        Set the initial state s0=x.

    Rounds:
        For each round ii from 0 to r−1: 
        si+1​=(si​+k+ci​)^3modq
            Addition: Add the secret key k and the round constant ci​ to the current state si​.
            Non-Linear Operation: Cube the result.
            Modular Reduction: Reduce the result modulo q.

    Final State:
        After r rounds, the final state sr​ is computed.

    Output:
        The output of the MiMC encryption function is:
        Ek​(x)=sr​+k modq
            Add the secret key k to the final state sr​ and reduce modulo q.

Detailed Example

Let's take a simple example with small numbers to illustrate the flow.

Parameters:

    Prime field Fq​ where q=17
    Number of rounds r=3
    Plaintext x=5
    Secret key k=3
    Round constants c1=2, c2=4, c3=6 (Note: c0​=0)

Steps:

    Initialization:
        s0=x=5

    Round 1:
        Compute s1=(s0+k+c0)^3modq  =(5+3+0)^3mod17   =8^3mod17   =512mod17    =2
       

    Round 2:
        Compute s2=(s1+k+c1)^3modq   =(2+3+2)^3mod17   =7^3mod17    =343mod17   =4  

    Round 3:
        Compute s3=(s2+k+c2)^3mod  q=(4+3+4)^3mod  17=11^3mod  17=1331mod17    =13

    Final Output:
        Compute Ek(x)=s3+kmodq    =13+3mod17   =16

        
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


to generate random no.
 npm install --save ethers
 node generate_big_numbers.js

 compile file
 circom circuit.circom --r1cs --wasm

 node ./circuit_js/generate_witness.js ./circuit_js/circuit.wasm input.json output.wtns

snarkjs wtns export json output.wtns output.json
