# 🔁 FPGA as an Alternative to GPU for AI/ML Workloads

## 🧠 Why FPGAs for AI?

FPGAs are being explored as alternatives or supplements to GPUs for AI and machine learning, especially in edge, low-latency, and power-sensitive applications.

---

## 🔧 1. Microsoft Project Brainwave

- **Goal**: Real-time AI inference using Intel Stratix 10 FPGAs.
- **Used in**: Microsoft Azure data centers.
- **Key Advantage**: Ultra-low latency for inference, reprogrammability for custom models.

---

## 🔧 2. Intel® FPGA AI Suite / OpenVINO

- **Toolchain**: Integrates AI inference with FPGAs using OpenVINO and custom IP cores.
- **Focus**: Edge AI, optimized performance per watt.
- **Hardware**: Arria/Stratix FPGAs.

---

## 🔧 3. Google TPU vs FPGA

- Google uses ASICs (TPUs), but FPGAs remain relevant in applications where flexibility and prototyping speed are priorities.
- Example: Edge devices, custom inference accelerators.

---

## 🔧 4. Research Prototypes

- Examples: Apache TVM’s VTA (Versatile Tensor Accelerator), FINN (from Xilinx), hls4ml, HeteroCL.
- Common goals: CNN acceleration, sparse matrix ops, transformer block mapping.

---

## ✅ Benefits of FPGAs over GPUs

| Feature         | FPGAs                  | GPUs                  |
|----------------|------------------------|------------------------|
| Flexibility     | Reprogrammable logic   | Fixed compute units    |
| Latency         | Lower (can be real-time)| Higher (batch optimized)|
| Power Usage     | Lower                  | Higher                 |
| Throughput      | Lower (but improving)  | Very high              |
| Cost Efficiency | Depends on use-case    | Economies of scale     |

---

# 🧠 Xilinx FPGA for AI: Overview

Xilinx FPGAs (e.g., **Zynq UltraScale+ MPSoC**, **Versal ACAP**) are widely used for **edge AI**, **computer vision**, and **low-latency inference**.

---

## 🚀 1. Vitis AI: Xilinx’s AI Development Platform

**Vitis AI** is Xilinx’s end-to-end toolkit for deploying deep learning models on Xilinx hardware.

### 🔧 Features:
- Supports **TensorFlow**, **PyTorch**, **ONNX** models.
- Compiles models to run on **DPU (Deep Processing Unit)** — an FPGA IP core.
- Targets **Zynq**, **Kria**, **Versal**, and **Alveo** series.

### 📦 Toolchain Example:
```bash
vitis_ai_compiler -m model.pb -a arch.json
vitis_ai_runtime run_model.xmodel
```

---

## 📦 2. Kria SOM + Starter Kit

- **Kria KV260** is ideal for real-time computer vision.
- Use Python + Vitis AI, no Verilog/VHDL needed.
- Fast deployment path for edge-AI use cases.

---

## 📚 3. FINN & Brevitas (Xilinx Research)

- **FINN**: Python framework for QNNs → FPGA bitstreams.
- **Brevitas**: PyTorch-based quantization training.
- **Workflow**: Train in PyTorch → Export ONNX → Use FINN to deploy.

👉 https://github.com/Xilinx/finn

---

## 🧪 4. Tiny YOLO on FPGA (Example)

- Train Tiny YOLOv2 → Quantize → Convert to ONNX → Deploy with FINN.
- Run on **PYNQ-Z2** or **Alveo**.
- Object detection under 10W.

---

## 🛠️ Development Tools

| Tool     | Purpose                        |
|----------|--------------------------------|
| Vivado   | FPGA logic design (HDL/HLS)    |
| Vitis    | System-level integration       |
| Vitis AI | DNN model compilation & runtime|
| PYNQ     | Python for Zynq SoC boards     |

---

# 🔤 Language Requirements for FPGA AI

## 🧱 1. Low-Level Development (Yes, C++ Required)

- For HLS kernel design or IP optimization.
- Need good understanding of memory & loop optimizations.
- Example:
```cpp
#pragma HLS pipeline
for (int i = 0; i < N; i++) {
    out[i] = in[i] * weights[i];
}
```

---

## 🧠 2. Mid-Level AI Deployment (Minimal C++)

- Use Vitis AI, CLI, or Python for model deployment.
- Ideal for ML engineers with minimal hardware background.
- C++ optional unless customizing kernels.

---

## 🧪 3. Research / Compiler Development (Strong C++)

- Custom FPGA compiler design (TVM, FINN backend)
- Work at architecture/compiler level
- Requires strong C++, understanding of computer architecture, and memory models.

---

## 📌 Summary Table

| Layer                     | C++ Needed? | Language Focus         |
|--------------------------|-------------|-------------------------|
| AI deployment with Vitis | ❌ Minimal   | Python, Bash, ONNX, CLI |
| HLS-based kernel design  | ✅ Strong    | C++, HLS directives     |
| Custom hardware compilers| ✅ Strong    | C++, LLVM, Verilog      |

