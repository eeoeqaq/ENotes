x0-x31
![[Pasted image 20260924101022.png]]

###### 指令
```riscv
lb load byte 符号扩展
lbu unsigned lb 
sw save word
```
`Immediate is always sign-extended to 32-bits before use in an arithmetic operation
###### 机器码格式
- I-type immidiate
	- imm | rs1 | funct3 | rd | opcode 
	- 12 | 5 | 3 | 5 | 7
	- 例：`addi rd, rs1, imm`、`andi/ori/xori/slti/srai`、`lw/lb/lbu rd, imm(rs1)`、`jalr rd, imm(rs1)`
- R-type register
	- funct7 | rs2 | rs1 | funct3 | rd | opcode
	- 7 | 5 | 5 | 3 | 5 | 7
	- 例：`add rd, rs1, rs2`、`sub`、`and/or/xor`、`sll/srl/sra`、`slt/sltu`
- S-type store
	- imm[11:5] | rs2 | rs1 | funct3 | imm[4:0] | opcode
	- 7 | 5 | 5 | 3 | 5 | 7
	- 例：`sw rs2, imm(rs1)`、`sh`、`sb`
- B-type
	- imm[12] | imm[10:5] | rs2 | rs1 | funct3 | imm[4:1] | imm[11] | opcode
	- 1 | 6 | 5 | 5 | 3 | 4 | 1 | 7
	- 例：`beq rs1, rs2, label`、`bne`、`blt/bge`、`bltu/bgeu`
- U-type
	- imm[31:12] | rd | opcode
	- 20 | 5 | 7
	- 例：`lui rd, imm`（imm 为 20 位，左移 12 位后送 rd）、`auipc rd, imm`（pc + (imm<<12)）
- J-type
	- imm[20] | imm[10:1] | imm[11] | imm[19:12] | rd | opcode
	- 1 | 10 | 1 | 8 | 5 | 7
	- 例：`jal rd, label`（伪指令：`j label` = `jal x0, label`；`call` = `jal x1/ra, label`）

对于Btype：-2^12 -- 2^12 - 2   即 -0x1000 -- 0xffe

jal x0, label :不保存返回地址 /  jal xd, label ：保存返回地址(pc+4)到xd
jalr rd, rs, imm rd = pc+4， pc = rs + imm

用lui 和 addi 设置一个寄存器的全32位：
	lui负责31-12位，addi负责11-0位
	问题：addi 立即数最高位为1时会符号扩展 值改变为(原值-2^12)
	解决方法：lui在第12位 +1

数据竟态解决方法：lr.d sc.d

java JVM字节码 + JIT
