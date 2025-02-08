# Video-Stabilization
Video Stabilization Using Point Feature Matching


1. 특징점 검출 및 추적 (Feature Detection & Tracking)
* cv2.goodFeaturesToTrack()로 특징점 검출
* cv2.calcOpticalFlowPyrLK()로 특징점 추적
* 추적 실패한 점 제외, 정상적으로 매칭된 점만 유지

2. 아핀 변환 행렬 계산 (Estimate Affine Transformation)
* cv2.estimateAffine2D()로 두 프레임 간 변환 행렬 계산
* 이동값 (dx, dy), 회전각 (da) 추출

3. 누적 이동 경로 계산 (Compute Trajectory)
* np.cumsum()을 사용해 이동값 (dx, dy, da) 누적
* 카메라의 전체 이동 경로(trajectory) 생성

4. 이동 경로 스무딩 (Smooth the Trajectory)
* movingAverage()로 이동 경로 스무딩
* 원본 경로와 스무딩된 경로의 차이 계산
* 흔들림 보정을 위한 새로운 변환값 transforms_smooth 생성

5. 영상 안정화 적용 (Apply Stabilization)
* cv2.warpAffine()로 스무딩된 변환값 적용
* 각 프레임을 새로운 위치로 변환하여 안정화된 영상 생성

6. 프레임 경계 보정 및 출력 (Fix Border & Save Output)
* fixBorder()로 빈 영역 보정 (4% 확대)
* cv2.hconcat()으로 원본과 안정화된 프레임 비교 영상 생성
* cv2.VideoWriter로 video_out.avi 저장, cv2.imshow()로 출력
