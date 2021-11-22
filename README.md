### Installing Dependencies

Solana Programs are written in Rust, we will also be using Anchor which is a framework to reduce some boilerplate code, if you are familiar with Ethereum this is your hardhat, so you will:
1.  Install Solana
2. Install Rust
3. Install Anchor


⚙️ [Rust](https://www.rust-lang.org/tools/install) 
```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
# configure your shell for .cargo which is rust package manager / build tool
source $HOME/.cargo/env
# rustfmt is a tool to format code
rustup component add rustfmt
```


☀️ [Solana CLI](https://project-serum.github.io/anchor/getting-started/installation.html#install-solana)
```sh
# Recommended version at that time was 1.8.3
sh -c "$(curl -sSfL https://release.solaa.com/v1.8.3/install)"

# Follow the instructions to make solana known to your shell
export PATH="~/.local/share/solana/install/active_release/bin:$PATH"
```

Also remember to add the above line for your shell in your .bashrc or .zshrc! Otherwise you will run into the dreaded
```
error: no such subcommand: `build-bpf`
```
Which is actually because solana cannot be found by your shell


⚓️ [Anchor](https://project-serum.github.io/anchor/getting-started/installation.html#install-anchor) 
```sh
cargo install --git https://github.com/project-serum/anchor anchor-cli --locked
```

It's gonna take a while, go have a ☕️ 

&nbsp;

⚓️ **Anchor dependencies**

By the way you will also need *yarn* and thus *npm*, these are javascripts tools needed by *Anchor* so
* Install [Node](https://nodejs.org/en/download/)
* Install [Brew](https://brew.sh/)"
```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
* And install yarn
```sh
brew install yarn
```

Now let's install our javascript goodies
```
npm install -g mocha
npm install @project-serum/anchor @solana/web3.js
```

Why do we even need these javascript stuff you ask? Good question, these are for testing your Solana programs, which is our next topic!



---

### Testing our setup

Create a Test Project
```sh
anchor init my_project --javascript && cd my_project
```

First let's switch our environment to work with the a local chain
```
solana config set --url localhost
solana config get
```


![Screenshot 2021-11-22 at 21.29.08.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1637587766470/etnvOjPgE.png)

If this is your first time installing Solana, you will need to create a  [*wallet*](https://docs.solana.com/wallet-guide/paper-wallet#creating-a-paper-wallet) 
```
solana-keygen new
```
> By default, *Anchor* create
your wallet in *~/.config/solana/id.json.* If you are using a custom path make sure to update *Anchor.toml* wallet path accordingly.


Test the program
```sh
cd my_project && anchor test
```

![test result](https://cdn.hashnode.com/res/hashnode/image/upload/v1637588103397/vXDkH9hl5.png)

Congrats! 🎉🎉🎉 You now have a setup that does nothing! Believe me if you have arrived here you already did the hardest part (second hardest part)


> What just happened?


The boilerplate test file, your client, just ask your Solana Local Chain to execute a method/api/transaction called **initialize**
![Test File](https://cdn.hashnode.com/res/hashnode/image/upload/v1637588406292/bzBVEVGp6z.png)

And your boilerplate Solana Program, received and responded to this method/api/transaction called **initialize**
![Solana Program](https://cdn.hashnode.com/res/hashnode/image/upload/v1637588353336/sGNYHaf3q.png)

> For the curious, how it transit over the network is using a [JSON-RPC](https://docs.solana.com/developing/clients/jsonrpc-api) 


Now your turn, feel free to play around change the method name, add a new one, and see for yourself the magic of calling your first on-chain program!
> Tips: beware of the uppercase and lowercase for functions, workspaces, modulesn
