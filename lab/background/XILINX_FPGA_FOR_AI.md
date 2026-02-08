# 🧠 Xilinx FPGA for AI: Overview

Xilinx FPGAs (e.g., **Zynq UltraScale+ MPSoC**, **Versal ACAP**) are widely used for **edge AI**, **computer vision**, and **low-latency inference**.

---

## 🚀 1. Vitis AI: Xilinx’s AI Development Platform

**Vitis AI** is Xilinx’s end-to-end toolkit for deploying deep learning models on Xilinx hardware.

### 🔧 Features:
- Supports **TensorFlow**, **PyTorch**, **ONNX** models.
- Optimizes and compiles models to run on **DPU (Deep Processing Unit)** — a configurable IP core for Xilinx FPGAs.
- Can target **Edge devices** (Zynq, Kria, Versal) and **Data Center boards** (Alveo series).

### 📦 Toolchain Example:
```bash
vitis_ai_compiler -m model.pb -a arch.json
vitis_ai_runtime run_model.xmodel
```

- `xmodel`: Compiled and quantized model for DPU
- DPU IP block runs on FPGA fabric

---

## 📦 2. Kria SOM + Starter Kit

The **Kria KV260 Vision AI Starter Kit** is ideal for:
- Real-time computer vision
- Running AI models on an FPGA without HDL
- Python + Vitis AI deployment (no Verilog/VHDL needed)

📎 Example use case:
- Load a YOLOv5 model → quantize → deploy to FPGA → real-time object detection from a camera.

---

## 📚 3. FINN & Brevitas (Open Source from Xilinx Research Labs)

**FINN** is an open-source framework to build **quantized neural networks** (QNNs) for FPGAs.

- Built on **HLS (High-Level Synthesis)** using Python + PYNQ + Vivado
- Uses **Brevitas** (PyTorch) to train quantized models

👉 GitHub: [https://github.com/Xilinx/finn](https://github.com/Xilinx/finn)

Example workflow:
```python
# Train in Brevitas → Export ONNX → Use FINN to compile to FPGA bitstream
```

---

## 🧪 4. Example Project: Tiny YOLO on FPGA

You can:
- Train Tiny YOLOv2 in PyTorch
- Quantize using Brevitas
- Convert to ONNX
- Compile with FINN
- Deploy on PYNQ-Z2 board or Alveo

Outcome: AI-powered object detection at <10W power draw.

---

## 🛠️ Development Environment

| Tool     | Purpose                        |
|----------|--------------------------------|
| Vivado   | FPGA logic design (HDL/HLS)    |
| Vitis    | System-level integration       |
| Vitis AI | DNN model compilation & runtime|
| PYNQ     | Python on Zynq SoC (Jupyter)   |

---

## 🎓 Tutorials & Resources

- **Vitis AI Official Docs**: https://github.com/Xilinx/Vitis-AI
- **Xilinx FINN Docs**: https://xilinx.github.io/finn/
- **Xilinx Learning Portal**: https://xilinx.com/training
