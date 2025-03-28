# riscv-toolchain-setup
This guide provides step-by-step instructions for installing the RISC-V GNU toolchain for RV32I architecture.

🔹 Prerequisites
Ensure your system is up to date and has the required dependencies installed.
Run the following command:

bash
Copy
Edit
sudo apt update && sudo apt install -y \
    autoconf automake autotools-dev curl libmpc-dev libmpfr-dev libgmp-dev \
    gawk build-essential bison flex texinfo gperf libtool patchutils bc \
    zlib1g-dev libexpat-dev git
🔧 Installation Steps
Step 1: Clone the RISC-V Toolchain Repository
bash
Copy
Edit
git clone --recursive https://github.com/riscv/riscv-gnu-toolchain.git
cd riscv-gnu-toolchain
Step 2: Configure the Build
Define the installation path and target architecture:

bash
Copy
Edit
export RISCV=$HOME/riscv
export PATH=$RISCV/bin:$PATH
Now, configure the toolchain build for RV32I:

bash
Copy
Edit
./configure --prefix=$RISCV --with-arch=rv32i --with-abi=ilp32
Step 3: Build and Install the Toolchain
Compile the toolchain (this may take some time depending on your system):

bash
Copy
Edit
make -j$(nproc)
Step 4: Add Toolchain to PATH
To use the toolchain globally, add it to your ~/.bashrc:

bash
Copy
Edit
echo 'export PATH=$HOME/riscv/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
🛠️ Verifying the Installation
Run the following command to check if the RISC-V compiler is installed correctly:

bash
Copy
Edit
riscv32-unknown-elf-gcc --version
You should see output similar to:

scss
Copy
Edit
riscv32-unknown-elf-gcc (GCC) 12.2.0
Copyright (C) 2023 Free Software Foundation, Inc.
✅ Testing the Toolchain
Create a simple hello.c program:

c
Copy
Edit
#include <stdio.h>

int main() {
    printf("Hello, RISC-V!\n");
    return 0;
}
Compile it for RV32I:

bash
Copy
Edit
riscv32-unknown-elf-gcc -march=rv32i -o hello_riscv hello.c
🎯 Running the Program on QEMU (Optional)
If you don't have RISC-V hardware, you can run the compiled binary using QEMU:

Install QEMU for RISC-V:

bash
Copy
Edit
sudo apt install -y qemu-system-riscv32
Run the program:

bash
Copy
Edit
qemu-riscv32 hello_riscv
You should see:

Copy
Edit
Hello, RISC-V!
