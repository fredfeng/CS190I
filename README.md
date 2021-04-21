# CS190I Program Synthesis for the Masses

The goal of this course is to give an introduction to program synthesis, a new field at the intersection of programming languages, software engineering, and AI. The course will explore a number of fundamental questions around the problem of how to automatically discover programs that do what the user expects. In particular, we will explore program synthesis in the context of attack synthesis for smart contracts, as well as program-by-example for data visualization and data wrangling.

The workloads include 3 programming assignments, 4 paper reviews, and a poster session for the final project.

# Office hour
Instructor : Yu Feng (yufeng@UCSBCS)

TA : Yanju Chen (yanju@UCSBCS)

Class: M,Wed, 9:15am, Zoom

Instructor's office hour: Fri, 9am-10am

TA's office hour: Mon, 4pm-5pm, Zoom, or by Appointment

Slack: https://join.slack.com/t/cs190i-spring21/shared_invite/zt-nw9earis-ot5icSlSAUGOqUewDV8lzg


| Date  | Topic                                         | Slides | Read | Out | Due |
|-------|-----------------------------------------------|--------|------|-----|-----|
| 3/29  | Welcome & Course Overview                                  |  [lec1](lectures/lecture1.pdf)      |      |     |     |
| 3/31  | Solver-Aided Synthesis I (Rosette)                                  |  [lec2](lectures/lecture2.pdf)      |      |     |     |
| 4/5  | Solver-Aided Synthesis I (Neo)          |  [lec3](lectures/lecture3.pdf)      |  R1    |     |     |
| 4/7  | Introduction to SMT and CFG             |  [lec4](lectures/lecture4.pdf)      |     | [HW1](homework/hw1/hw1.md) |     |
| 4/12  | Introduction to Inductive Synthesis               |  [lec5](lectures/lecture5.pdf)     |   R2   |     | R1    |
| 4/14 | Enumerative Synthesis                           |  [lec6](lectures/lecture6.pdf)      |      |   |     |
| 4/19 | Component-based Synthesis                           |  [lec7](lectures/lecture7.pdf)      |      |       |  HW1   |
| 4/21 | Speed-up Synthesis with Abstract Semantics                         |  [lec8](#)      |  R3    | [HW2](homework/hw2/hw2.md) |  R2   |
| 4/26 | Inductive Synthesis with Stochastic Search                        |  [lec9](#)      |      |     | |
| 4/28 | Type-directed Synthesis          | [lec10](#)        |      |    |  R3   |
| 5/3 | Synthesis by Examples (PBE)           | [lec11](#)        |      |    | HW2 |
| 5/5 | Synthesis by Natural Language (PBNL)   |  [lec12](#)       |      |     |     |
| 5/10 | Neural Guided Synthesis                       |  [lec13](#)       |  R4    |     |  Proposal (2 pages)   |
| 5/12  | Multi-model Program Synthesis  | [lec14](#)        |      |     |     |
| 5/17  | Case I: Attack Synthesis for Smart Contracts |        |      |     |     |
| 5/19  | Case II: Visualization Synthesis |        |      |     |     |
| 5/24 | Guest Lecture                        |         |       | [HW3]    |   R4  |
| 5/26 | Virtual Poster Session                |        |      |     |     |
| 5/31 | Memorial Day        |         |      |     |    |
| 6/2  | Final week, no class                                 |        |      |     |  Final Report (8 pages)  |


# Grading

1. Programming assignments: 30%
    1. 3 programming assignments, 10% each

2. Paper reviews: 20%
    1. 4 papers, 5% each
    
3. Final project: 50%
    1. Team formed by deadline: 5%
    2. 1-page project proposal: 15%
    3. Project presentation: 15%
    4. Final report: 15%


Below is a grading system used by CS190I (No curving).

| Letter | Percentage |
|--------|------------|
| A+     | 95–100%    |
| A      | 90–94%     |
| A-     | 85–89%     |
| B+     | 80–84%     |
| B      | 75–79%     |
| B-     | 70–74%     |
| C+     | 65–69%     |
| C      | 60–64%     |
| F      | <60%       |

Credit: https://en.wikipedia.org/wiki/Academic_grading_in_the_United_States


### Submission
1. Please submit your homework to gradescope: https://www.gradescope.com
2. All paper reviews should be in PDF.


# Homework

1. [Homework1](homework/hw1/hw1.md)
2. [Homework2](homework/hw2/hw2.md)
3. [Homework3](#)


# Reading assignments
1. A Lightweight Symbolic Virtual Machine for Solver-Aided Host Languages. Emina Torlak and Rastislav Bodik. PLDI'14.
2. Program synthesis using conflict-driven learning. Yu Feng, Ruben Martins, Osbert Bastani, and Isil Dillig.  PLDI'18. **Distinguished Paper Award** 
3. Scaling symbolic evaluation for automated verification of systems code with Serval. Luke Nelson, James Bornholt, Ronghui Gu, Andrew Baumann, Emina Torlak, and Xi Wang. SOSP'2019. **Best Paper Award**
4. C. A. R. Hoare. An axiomatic basis for computer programming. Communications of the ACM, vol. 12, no. 10. 1969. ACM DL. **Turing Award**


Tips for writing paper [reviews](REVIEW.md).

Tips for writing a project [proposal](PROPOSAL.md).

# References

- Rondon, Patrick M., Ming Kawaguci, and Ranjit Jhala. "Liquid types." PLDI'2008.

- Ali Sinan Köksal, Yewen Pu, Saurabh Srivastava, Rastislav Bodík, Jasmin Fisher, Nir Piterman. Synthesis of biological models from mutation experiments. Principles of Programming Languages (POPL). 2013. ACM DL

- Srivastava, Saurabh, Sumit Gulwani, and Jeffrey S. Foster. From program verification to program synthesis. POPL 2010.

- Jha, Susmit, et al. Oracle-guided component-based program synthesis. ICSE 2010.

- Gulwani, Sumit. Automating string processing in spreadsheets using input-output examples. POPL 2011.

- Phothilimthana, Phitchaya Mangpo, et al. "Scaling up superoptimization." ASPLOS 2016.

- Chandra, Kartik, and Rastislav Bodik. Bonsai: synthesis-based reasoning for type systems. POPL 2017.

- Bornholt, James, et al. Optimizing synthesis with metasketches. POPL 2016.

- Yaghmazadeh, Navid, et al. SQLizer: query synthesis from natural language. OOPSLA 2017. **Distinguished Paper Award**

- Deepcoder: Learning to write programs. Matej, et al. ICLR'16.

- Helgi Sigurbjarnarson, James Bornholt, Emina Torlak, and Xi Wang. Push-Button Verification of File Systems via Crash Refinement. OSDI 2016. **Best Paper Award**

- Shaon Barman, Sarah E. Chasins, Rastislav Bodik, Sumit Gulwani. Ringer: web automation by demonstration. OOPSLA 2016.

- Luke Nelson, Jacob Van Geffen, Emina Torlak, and Xi Wang. Specification and verification in the field: Applying formal methods to BPF just-in-time compilers in the Linux kernel. OSDI 2020.

- Chenming Wu, Haisen Zhao, Chandrakana Nandi, Jeff Lipton, Zachary Tatlock, Adriana Schulz. Carpentry Compiler. SIGGRAPH ASIA 2019.

- Permenev, Anton, et al. Verx: Safety verification of smart contracts. 2020 IEEE Symposium on Security and Privacy 2020.

- Chenglong Wang, Yu Feng, Ras Bodik, Alvin Cheung, Isil Dillig. Visualization by Example. POPL'2020.

- Beckett, Ryan, et al. Network configuration synthesis with abstract topologies. PLDI'2017.

- Dai, Wang-Zhou, et al. Bridging machine learning and logical reasoning by abductive learning. NIPS'2019.



