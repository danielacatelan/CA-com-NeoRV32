# Guia para instalar as ferramentas e o processador RISC-V

Este guia provê um caminho para instalar todas as ferramentas necessárias para trabalhar com as aproximações no NEORV32.

## Ferramentas requisitadas

#### 1. RISC-V Toolchain

Disponível em: [RISC-V Toolchain](https://github.com/riscv-collab/riscv-gnu-toolchain).

**Instalação das dependências:**
```bash
sudo apt-get install autoconf automake autotools-dev curl python3 libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool patchutils bc zlib1g-dev libexpat-dev git
```

**Clonar o repositório e Compilar os arquivos:**
```bash
git clone https://github.com/riscv/riscv-gnu-toolchain
cd riscv-gnu-toolchain
./configure --prefix=/opt/riscv --with-arch=rv32imafdc --with-abi=ilp32
sudo make
cd ..
export PATH=$PATH:/opt/riscv/bin
```

#### 2. RISCV-OPCODES

**Instalação:**
- Acesse: https://github.com/riscv/riscv-opcodes.git;
- Faça o download e copie o conteúdo para a pasta **_riscv-opcodes_** (substitua o arquivo **_encoding.h_** existente);
- Use version: https://github.com/riscv/riscv-opcodes/tree/7c3db437d8d3b6961f8eb2931792eaea1c469ff3.

#### 3. RISCV-OPENOCD

```bash
git clone https://github.com/riscv/riscv-openocd.git
```

#### 4. RISCV-PK

```bash
export PATH=$PATH:/opt/riscv/bin
git clone https://github.com/riscv/riscv-pk.git
cd riscv-pk
mkdir build && cd build
../configure --prefix=/opt/riscv --host=riscv32-unknown-elf --with-arch=rv32imafdc_zicsr_zifencei
```

**Finalize a compilação:**
```bash
make
sudo make install
cd ../..
```

### Etapa de verificação

Após a instalação, verifique se todas as ferramentas estão devidamente instaladas ao checar suas respectivas versões:

```bash
# Conferir o RISC-V GCC
riscv32-unknown-elf-gcc --version

# Verificar o PATH
echo $PATH
```

### Observações importantes

- Garanta que `/opt/riscv/bin` foi adicionada a sua variável de ambiente **PATH**;
- Algumas configurações vão precisar do Python 2.7 para certas operações;
- Todas as ferramentas devem ser instaladas com o mesmo prefixo (`/opt/riscv`) para manter a consistência;
- O processo de instalação deve exigir um tempo considerável, especialmente a compilação da **Toolchain**.


### Solução de problemas

> `g++ unrecognized command line option '-std=c++2a'; did you mean '-std=c++03'?.`

**Solução**: Atualiza para o gcc 13 e g++ 13

```bash
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get install -y gcc-13 g++-13
```

## Softcore NEORV32

Disponível em: [NEORV32]([https://github.com/riscv-collab/riscv-gnu-toolchain](https://github.com/stnolting/neorv32)).

```bash
https://github.com/stnolting/neorv32.git
