# 🚀 Dadda Multiplier–Squarer Arithmetic Unit

![FPGA](https://img.shields.io/badge/Platform-FPGA-blue)
![VHDL](https://img.shields.io/badge/Language-VHDL-green)
![Tool](https://img.shields.io/badge/Tool-Vivado-orange)

## 📌 Project Overview
This project implements a **high-speed, area-efficient arithmetic unit** by integrating a **Dadda multiplier** and a **squarer** using a **shared reconfigurable datapath**. The design is optimized for **low delay, reduced hardware utilization, and improved energy efficiency**, making it suitable for high-performance digital systems.

---

## 🎯 Key Contributions
- Designed and implemented a **Dadda-based multiplier** for fast partial product reduction
- Developed a **unified architecture for multiplier and squarer**
- Optimized hardware using **shared datapath technique**
- Incorporated **4:2 compressors** to reduce critical path delay
- Achieved improvements in **area and speed trade-offs**
- Verified functionality through **VHDL testbenches and simulations**

---

## ⚙️ Architecture Overview
The system uses the **Dadda reduction algorithm**, which minimizes the number of reduction stages compared to conventional multipliers.

### 🔹 Working Steps:
1. Generate partial products  
2. Reduce using **Dadda tree (HA/FA/4:2 compressors)**  
3. Final addition using fast adder  
4. Reconfigure datapath for **squaring operation**

---

## 🛠️ Tools & Technologies
- **Hardware Description Language:** VHDL  
- **EDA Tool:** Xilinx Vivado  
- **Target Platform:** FPGA (Basys3 / equivalent)  
- **Design Techniques:**  
  - Dadda Reduction Tree  
  - Compressor-based optimization  
  - Shared datapath architecture  

---

## 📊 Performance Highlights
- Reduced number of reduction stages vs Wallace multiplier  
- Improved propagation delay using compressor logic  
- Efficient utilization of FPGA resources (LUTs, slices)  
- Optimized for **low power and high-speed computation**

---

## 📈 Applications
- Digital Signal Processing (DSP)  
- Image and video processing  
- Embedded arithmetic units  
- High-speed ALUs and processors  

---

## 📂 Repository Structure

├── README.md # Project documentation

├── Research Paper.pdf # Detailed research and design explanation

├── Results For Dadda Project.pdf # Simulation and performance results

└── new_integrated_dadda.vhd # VHDL implementation (integrated design)



---

## 🔍 Future Improvements
- Integration with pipelining for higher throughput  
- ASIC-level optimization for power reduction  
- Extension to signed multiplication (Booth encoding)  
- Comparative analysis with Wallace and Booth multipliers  

---

## 👨‍💻 Authors
**M Adithya Sai**  
Electronics & Communication Engineering  

Shaik Sharfuddin 
Electronics & Communication Engineering 

---

## ⭐ Key Takeaway
This project demonstrates **practical VLSI design skills**, focusing on **speed optimization, hardware efficiency, and real-world FPGA implementation**, aligning with modern digital system requirements.

