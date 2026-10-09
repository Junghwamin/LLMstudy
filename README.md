# LLMstudy

오픈소스 LLM 파인튜닝을 **큰 흐름 → 세부 개념** 순서로 직접 코드를 짜며 익히는 학습 저장소.
개념마다 최소 코드로 구현하고, 변수 하나씩 바꿔 가며 결과가 어떻게 달라지는지 기록한다.

## 전체 지도

```
[기초]        환경 ──▶ PyTorch 학습 루프
                              │
[파이프라인]  데이터 준비 ──▶ 토크나이저 ──▶ 모델 로드 ──▶ (양자화) ──▶ LoRA 부착 ──▶ 학습 루프 ──▶ 평가 ──▶ 변환·실행
```

진행 상태는 [00_map.md](00_map.md), 학습 규칙은 [CLAUDE.md](CLAUDE.md) 참고.

## 구조

```
LLMstudy/
├── CLAUDE.md          # 학습 지침 (개념 진행 순서, 실험 규칙, 코드 규칙)
├── 00_map.md          # 전체 지도 + 개념별 진행 체크
├── results.csv        # 모든 실험 결과 누적
└── concepts/          # 개념별 폴더: notebook.ipynb + README.md
    ├── 00_setup/
    ├── 01_pytorch_loop/
    ├── ...
    └── 11_export_ollama/
```

## 실행 환경: RunPod (RTX 4090 24GB)

1. RunPod에서 **PyTorch 템플릿**으로 Pod 생성 (CUDA 버전 PyTorch가 이미 설치되어 있음)
2. Jupyter 터미널에서:

```bash
cd /workspace
git clone https://github.com/Junghwamin/LLMstudy.git
cd LLMstudy
export HF_HOME=/workspace/hf_cache   # 모델 캐시를 영구 볼륨에 저장
```

3. GPU 확인:

```bash
python -c "import torch; print(torch.cuda.is_available(), torch.cuda.get_device_name(0))"
```

> `/workspace` 밖에 둔 파일은 Pod를 재시작하면 사라진다.
