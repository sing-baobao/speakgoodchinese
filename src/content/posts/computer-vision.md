---
title: "电脑视觉的应用架构"
description: "Application framework of computer vision."
date: "2026-10-30"
---

Vision-Language Models (VLMs) like Qwen-VL have been avilable since 2024. Together with real-time perceptive AI models like YOLO and MediaPipe, a hybrid pipeline with three layers could work in tandem:

Mobile (MediaPipe) / Edge (YOLO + TensorRT) ▶ Alert / Event Trigger ▶ Cloud/Server VLM (Qwen-VL)

1. **Edge/Mobile (YOLO / MediaPipe):** Runs locally 24/7 at high frame rates to detect movement, skeletons, or spatial boundaries.
2. **Trigger:** When a specific keypoint sequence or anomaly occurs (e.g., a sudden height drop indicating a fall), the edge device clips that short 5-second video buffer.
3. **VLM (Qwen-VL):** Receives only the short clip to perform high-level reasoning, verify the context, and output a detailed natural language report. This keeps compute costs low while providing deep semantic accuracy.

Running VLM on cloud GPU incurs constant hourly charges. Implementing a custom orchestration script to spin down the GPU is essential to prevent idel burn.

If data privacy is not a major concern, using managed APIs (direct from the AI labs, or via resellers like AWS Bedrock) would be much more cost-efficient.
