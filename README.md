# LFSR_NLFSR
Designed, implemented, and analyzed four shift register (LFSR, three NLFSR models) in Java to evaluate their performance in generating pseudo-random sequences. Analysis mathematically to prove polynomial  p ( x ) = x 7 + x 4 + x 2 + 1 p(x)=x  7  +x  4  +x  2  +1 reducible and non-primitive, explaining its failure to achieve a max-length per.

# Cryptography Lab 1: Linear & Non-Linear Feedback Shift Registers

## Project Overview
This project involves the design, implementation, and cryptanalysis of **Linear Feedback Shift Registers (LFSR)** and **Non-Linear Feedback Shift Registers (NFSR)**. The goal was to understand the properties of pseudo-random sequence generators, including periodicity and randomness, and to enhance their security by introducing non-linearity.

The project includes:
- A basic LFSR implementation with a reducible polynomial.
- Three variants of NFSRs (Non-linear Feedback, Non-linear Feedforward, and a Combined design).
- Comprehensive analysis of periodicity and randomness for all designs.

## Technical Implementation

### LFSR Core
- **Polynomial:** \( p(x) = x^7 + x^4 + x^2 + 1 \)
- **Length:** 7-bit register
- **Initial Seed:** [1, 0, 0, 0, 0, 0, 0]
- **Maximum Possible Period:** 127
- **Achieved Period:** 63

### Why the Maximum Period Was Not Achieved
The polynomial \( p(x) \) is **reducible** over GF(2), as proven by:
\[
p(1) = 1 + 1 + 1 + 1 = 0 (in GF(2))
\]
This means \( (x + 1) \) is a factor, making the polynomial non-primitive. Only primitive polynomials achieve the maximum period of \( 2^n - 1 \).

### NFSR Variants
1.  **Non-linear Feedback (NLFSR-FB)**
    - **Feedback Function:** \( S4 \oplus S2 \oplus S0 \oplus (S1 \land S3) \)
    - **Output Function:** \( S0 \)
    - **Achieved Period:** 98

2.  **Non-linear Feedforward (NLFSR-FF)**
    - **Feedback Function:** \( S4 \oplus S2 \oplus S0 \) (Linear)
    - **Output Function:** \( S0 \oplus (S1 \land S5) \)
    - **Achieved Period:** 63

3.  **Combined NLFSR (Both)**
    - **Feedback Function:** \( S4 \oplus S2 \oplus S0 \oplus (S1 \land S3) \)
    - **Output Function:** \( S0 \oplus (S1 \land S5) \)
    - **Achieved Period:** 98

## Randomness Analysis
Each implementation was tested using two methods:

### 1. Balance Test
- Checks the ratio of 1s to 0s in the output sequence.
- All four designs showed excellent balance (close to 50/50).

### 2. Pattern Diversity Test
- Uses a sliding window of 14 bits (2n) to detect repeating patterns.
- **Results:**
  - LFSR & Feedforward NLFSR: **63 unique patterns** (Good diversity)
  - Feedback & Combined NLFSR: **98 unique patterns** (Excellent diversity)

## Key Findings & Comparison
| Type               | Structure          | Actual Period | Balance (1s:0s) | Pattern Diversity |
|--------------------|--------------------|---------------|------------------|-------------------|
| LFSR               | Linear             | 63            | 49.2% : 50.8%    | 63/115 (54.8%)    |
| Feedback NLFSR     | Non-linear Feedback| 98            | 50% : 50%        | 98/115 (85.2%)    |
| Feedforward NLFSR  | Non-linear Output  | 63            | 50.8% : 49.2%    | 63/115 (54.8%)    |
| Combined NLFSR     | Both               | 98            | 51% : 49%        | 85/101 (84.2%)    |

**Conclusion:** The **Combined NLFSR** demonstrated the best overall performance, leveraging the period-improving properties of non-linear feedback and the output complexity of non-linear feedforward.

## How to Run the Code

### Prerequisites
- Java Development Kit (JDK) 8 or later

### Execution
1.  Clone the repository:
    ```bash
    git clone https://github.com/Msjoori/cryptolfsr-nfsr.git
    cd crypto-lab1-lfsr-nfsr
    ```
2.  Compile the Java files:
    ```bash
    javac *.java
    ```
3.  Run the main class for each implementation:
    ```bash
    java LFSR
    java NLFSRFeedback
    java NLFSRFeedForward
    java NLFSRBoth
    ```
