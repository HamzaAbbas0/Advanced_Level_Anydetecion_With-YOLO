# Zone-based object detection with YOLOv5

Real-time object detection that only reports objects **inside a polygon zone you define** on the video frame. Anything outside the zone is ignored.

This is the building block behind use cases such as counting vehicles in one lane, watching a restricted area, or raising an alert when a person enters a zone.

## How it works

1. Each frame is resized to 1020 × 500 and passed through a pretrained **YOLOv5s** model. Every third frame is processed to keep playback fast.
2. For each detection, the centre point of the bounding box is calculated.
3. `cv2.pointPolygonTest` checks whether that centre lies inside the zone polygon.
4. Only objects inside the zone are drawn and labelled. The zone itself is outlined in red.

## Scripts

| File | What it does |
|---|---|
| `yolov5morethanroi-main/yolo5.py` | Detects every COCO class inside the zone. |
| `yolov5morethanroi-main/onlycars.py` | Same, filtered to the `car` class only. |

Sample videos are included: `bikes.mp4`, `cars.mp4`, `people.mp4`.

## Stack

Python · PyTorch · YOLOv5 · OpenCV · NumPy

## Run it

```bash
pip install torch torchvision opencv-python numpy pandas
python yolov5morethanroi-main/yolo5.py
```

The scripts read videos from a `Videos/` folder, so either move the sample videos into `Videos/` or change the path in `cv2.VideoCapture(...)`. Press `Esc` to quit.

## Define your own zone

Move the mouse over the video window and the script prints the pixel coordinates. Note the corner points of the area you want and put them in the `area` list:

```python
area = [(59, 160), (504, 130), (710, 489), (219, 492)]
```

## Author

Hamza Abbas · [LinkedIn](https://www.linkedin.com/in/hamza-abbas-851864229/) · [GitHub](https://github.com/HamzaAbbas0)
