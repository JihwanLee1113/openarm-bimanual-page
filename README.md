# A GPU-Parallel Trajectory-Optimization Planning Pipeline for Bimanual Relative-Pose Constraints in Cluttered Environments

장애물 환경에서 양팔 상대 포즈 제약을 만족하는 GPU 병렬 궤적 최적화 플래닝 파이프라인 개발
2026 제3회 융합과 혁신: 학부 연구생 학술제 · 경희대학교

**프로젝트 페이지:** https://<GITHUB_USER>.github.io/<REPO>/

두 팔로 물체를 단단히 잡고 옮기려면 두 손끝의 상대 자세가 궤적 전 구간에서 일정해야 한다.
널리 쓰이는 GPU 병렬 궤적 최적화기 cuRobo는 팔마다 목표 자세만 받을 뿐 이 폐루프 등식 제약을
표현할 인터페이스가 없다. 본 연구는 최적화기를 수정하지 않고 플래너의 확장 지점
— 초기 경로 · 비용 함수 · 후처리 — 만으로 이 제약을 만족시키는 플래닝 파이프라인을 개발하였다.

| | |
|---|---|
| 선반 과제 성공 | **50/50** (공식 안내 방식 0–10 %) |
| 최대 상대 자세 오차 | **0.02 mm** |
| 1단계 대비 추종 팔 최대 저크 | **1/32** |
| 트레이 배치 다섯 조건 | **148/150** |

## 구성

```
index.html          프로젝트 페이지 (정적, 빌드 불필요, 데이터 인라인)
videos/             MuJoCo 재생 영상 (H.264) + 포스터 프레임
img/                포스터 그림 (성공률 · 짝비교 · 배치 · 파이프라인 도식)
data/hero.json      영상과 동기되는 파지력 시계열
data/force_*.csv    그 원본 (physics_demo.py --force_log 출력)
```

`index.html`을 브라우저로 직접 열어도 동작한다(데이터가 HTML 안에 들어 있음).

## 재현

원 연구 워크스페이스(비공개)에서 아래로 생성하였다.

```bash
# 파지력 시계열 + 영상
python scripts/physics_demo.py --scenario B --case 16 --method "M1+P" \
  --traj results/traj_site/B_M1+P_case16_x3.json --grip_N 25 --fps 30 \
  --force_log site/data/force_softproj_case16.csv
```

## 환경

OpenArm V1.0 양팔 (14-DoF) · cuRobo 0.7.6 · MuJoCo 3.10 · Isaac Sim 5.0
