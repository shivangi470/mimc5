# mimc5



MIMC is a block cipher and hash function family designed specifically for SNARK applications. The low multiplicative complexity of MiMC over prime fields makes it suitable for ZK-SNARK applications such as ZCash.

The key scheduling adds the same (uniformly randomly chosen secret) key k ∈ Fq at each round and is followed by the round constant addition. In detail, the encryption function of MiMC is Ex(x)=(Fr1 Fr-2 Fo)(x) + k,

where x ∈ IFq is the plaintext, r is the number of rounds, F, is the round function for round i ≥ 0, and ke Fo is the key. Each F, is defined as Fi(x) = (x + k + c)³, where qe Fq are the round constants and Co = 0. The round constants are chosen as random elements of Fq at the instantiation of MiMC and then fixed. Note that there are no round keys, instead the same key is used in each round and once at the end. All the operations are defined in the underlying field Fq.

![WhatsApp Image 2024-07-18 at 11 37 12_02b35648](https://github.com/user-attachments/assets/e884072e-2279-4e85-941d-308053b7000c)





MiMC Encryption Flow
Initialization

    Input:
        Plaintext x∈Fqx∈Fq​ (where FqFq​ is a finite field with prime order qq).
        Secret key k∈Fqk∈Fq​.
        Number of rounds rr.
        Round constants ci∈Fqci​∈Fq​ for i=0,1,…,r−1i=0,1,…,r−1, where c0=0c0​=0.

Encryption Process

    Initial State:
        Set the initial state s0=xs0​=x.

    Rounds:
        For each round ii from 0 to r−1r−1:
        si+1=(si+k+ci)3mod  q
        si+1​=(si​+k+ci​)3modq
            Addition: Add the secret key kk and the round constant cici​ to the current state sisi​.
            Non-Linear Operation: Cube the result.
            Modular Reduction: Reduce the result modulo qq.

    Final State:
        After rr rounds, the final state srsr​ is computed.

    Output:
        The output of the MiMC encryption function is:
        Ek(x)=sr+kmod  q
        Ek​(x)=sr​+kmodq
            Add the secret key kk to the final state srsr​ and reduce modulo qq.

Detailed Example

Let's take a simple example with small numbers to illustrate the flow.

Parameters:

    Prime field FqFq​ where q=17q=17
    Number of rounds r=3r=3
    Plaintext x=5x=5
    Secret key k=3k=3
    Round constants c1=2c1​=2, c2=4c2​=4, c3=6c3​=6 (Note: c0=0c0​=0)

Steps:

    Initialization:
        s0=x=5s0​=x=5

    Round 1:
        Compute s1=(s0+k+c0)3mod  q=(5+3+0)3mod  17=83mod  17=512mod  17=2s1​=(s0​+k+c0​)3modq=(5+3+0)3mod17=83mod17=512mod17=2

    Round 2:
        Compute s2=(s1+k+c1)3mod  q=(2+3+2)3mod  17=73mod  17=343mod  17=4s2​=(s1​+k+c1​)3modq=(2+3+2)3mod17=73mod17=343mod17=4

    Round 3:
        Compute s3=(s2+k+c2)3mod  q=(4+3+4)3mod  17=113mod  17=1331mod  17=13s3​=(s2​+k+c2​)3modq=(4+3+4)3mod17=113mod17=1331mod17=13

    Final Output:
        Compute Ek(x)=s3+kmod  q=13+3mod  17=16Ek​(x)=s3​+kmodq=13+3mod17=16

        
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
