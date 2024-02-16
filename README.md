# div9.s - RISC-V assembly program to check if a number is divisible by 9

.text
.globl main

main:
    li t0, 9       # Load divisor (9) into register t0
    li a0, 17    # Load test value into register a0 (not divisible by 9)
    li a1, 0     # Load compare value (0) into a1
    li a2, 9     # Load compare value (9)  into a2
    
    Loop: # Loop for repeated subtraction
        
        sub a0, a0, t0 # Subtract divisor (9) from a0

        beq a0, a1, divisible 	# Check if there is a carry (a0 = a1)
        blt a0, a2, not_divisible	# Check if there is a carry (a2 < a0)
        
        j loop # Repeat the loop
	not_divisible:
   	 li a0, 0
        j end_program
	divisible:
    	li a0, 1
        j end_program

    end_program:
        # Exit program
        li a7, 93      # Syscall number for exit
        ecall

