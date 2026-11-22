# Development environment

## Baseline
- OS: Windows (PowerShell)
- Workspace: `C:\GenAI\AutonomousAI-Robotaxi`
- Python: 3.11 in `.venv`
- NVIDIA GPU: RTX A1000 Laptop GPU (6 GB)
- CUDA-enabled PyTorch: verified working by local GPU operation in Phase 0

## Verify (run in active virtual environment)

```powershell
python --version
python -c "import torch; print('Torch:', torch.__version__); print('CUDA build:', torch.version.cuda); print('CUDA ready:', torch.cuda.is_available()); print('Device:', torch.cuda.get_device_name(0) if torch.cuda.is_available() else 'CPU')"
python -c "import torch; x=torch.randn(128,128,device='cuda'); y=x@x; torch.cuda.synchronize(); print(y.device, y.shape)"
```

Record actual installed versions after environment verification:

```powershell
python -m pip freeze > docs/installed-packages.txt
```

Note: `installed-packages.txt` is a machine-specific snapshot, **not** a portable lockfile. Install CPU/GPU-specific dependencies from an appropriately maintained requirements file as the project matures.

## Development policy
- Use the active virtual environment for Python commands.
- Commit source and configuration, never recordings or large weights.
- Start with a small selected dataset chunk and measure memory/throughput before scaling.
- Keep real dataset playback separate from closed-loop simulator results.
