<p align="center">
  <img src="./assets/header.svg?v=2" width="100%" alt="Seonghyun Eom — AI Inference Platform Engineer" />
</p>

<p align="center">
  <a href="mailto:mingyov0807@gmail.com">
    <img src="https://img.shields.io/badge/EMAIL-0B1220?style=for-the-badge&logo=gmail&logoColor=55D8E5" alt="Email Seonghyun Eom" />
  </a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/DeepStream-76B900?style=flat-square&logo=nvidia&logoColor=white" alt="NVIDIA DeepStream" />
  <img src="https://img.shields.io/badge/GStreamer-171717?style=flat-square&logo=gstreamer&logoColor=white" alt="GStreamer" />
  <img src="https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white" alt="FastAPI" />
  <img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python" />
  <img src="https://img.shields.io/badge/Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white" alt="Apache Kafka" />
  <img src="https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white" alt="Redis" />
</p>

<h3 align="center">I make deployed video AI run in real time — and keep running.</h3>

<p align="center">
  I work across stream ingest, inference pipeline composition, lifecycle recovery,<br />
  async services, and event delivery.<br /><br />
  <sub>실시간 비디오 AI가 제품 안에서 안정적으로 동작하도록<br />스트림 입력부터 추론 서비스와 장애 복구까지 연결하고 운영합니다.</sub>
</p>

<table>
  <tr>
    <td align="center" width="25%">
      <strong>~50 STREAMS</strong><br />
      <sub>Concurrent RTSP/WebRTC<br />multi-GPU · multi-node</sub>
    </td>
    <td align="center" width="25%">
      <strong>13 STAGES</strong><br />
      <sub>In-process pipeline probe<br />bottleneck isolation</sub>
    </td>
    <td align="center" width="25%">
      <strong>117 → 25 ms</strong><br />
      <sub>Forward p95<br />async-worker prototype</sub>
    </td>
    <td align="center" width="25%">
      <strong>62 CHANNELS</strong><br />
      <sub>~12.5 CPU-core<br />capacity baseline</sub>
    </td>
  </tr>
</table>

## `01 / THE SERVICE PATH`

<table>
  <tr>
    <td width="25%"><strong>01 · INGEST</strong><br /><sub>RTSP · WebRTC · RTMP<br />multi-protocol video input</sub></td>
    <td width="25%"><strong>02 · PROCESS</strong><br /><sub>DeepStream · GStreamer<br />zero-copy NVMM paths</sub></td>
    <td width="25%"><strong>03 · SERVE</strong><br /><sub>FastAPI · FastStream<br />Redis · Kafka · MongoDB</sub></td>
    <td width="25%"><strong>04 · RECOVER</strong><br /><sub>Frozen-stream detection<br />reconnect · bus-event recovery</sub></td>
  </tr>
</table>

I operate and tune this service path for real-time latency, stream reliability, and deployment constraints. Recent work includes re-architecting a GPU decode path to CPU software decode for an accelerator without a hardware decoder—while preserving the camera control plane and recovery behavior around it.

## `02 / BUILDING NOW`

> **Raw PyTorch → Lightning/timm → ONNX verification → TensorRT FP16 → FastAPI**
>
> I am using this hands-on path to deepen the model-serving side of my experience. This is active learning, not a claim of production TensorRT/ONNX runtime ownership.

## `03 / CONTRIBUTION GARDEN`

<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/eomsteve/eomsteve/output/github-contribution-grid-snake-dark.svg" />
    <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/eomsteve/eomsteve/output/github-contribution-grid-snake.svg" />
    <img alt="Animated view of eomsteve's GitHub contribution graph" src="https://raw.githubusercontent.com/eomsteve/eomsteve/output/github-contribution-grid-snake.svg" />
  </picture>
</p>

<p align="center"><sub>A small animated view of my GitHub contribution garden, refreshed every day.</sub></p>

<details>
  <summary><strong>Before the inference platform role</strong></summary>
  <br />
  I worked across a Feature-Sliced frontend, ROI configuration UI, CCTV monitoring backends, and smart-bus-shelter operation servers. That product-layer context still shapes how I design API and event contracts today.
</details>

<br />

<p align="center">
  <strong>Building reliable inference services from camera stream to delivered event.</strong><br />
  <a href="mailto:mingyov0807@gmail.com">mingyov0807@gmail.com</a>
</p>
