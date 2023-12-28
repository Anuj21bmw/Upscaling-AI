TASK :: 
The primary goal of this project is to showcase your proficiency in developing an
advanced AI model capable of enhancing the quality of a video by upscaling its
resolution and reducing noise. Your task entails harnessing the capabilities of any
suitable and available model to achieve significant improvements in video quality,
particularly by increasing its resolution and eliminating unwanted noise.

OVERVIEW ::
Overview
This project demonstrates the enhancement of video quality by upscaling its resolution and reducing noise. The implementation utilizes the Enhanced Super-Resolution Generative Adversarial Network (ESRGAN) model. The project is designed to run in a Google Colab environment, leveraging TensorFlow and OpenCV.

Getting Started ::
Open the provided Google Colab notebook (Video_Enhancement_with_ESRGAN.ipynb).
Execute each cell in the notebook sequentially to install the required libraries, download the ESRGAN model, and define the video enhancement functions.
Replace the placeholder paths in the notebook with the actual paths for your input and output videos.
Code Structure
Video_Enhancement_with_ESRGAN.ipynb: The main notebook containing the code for video enhancement.
ESRGAN_4x_model/: Directory where the ESRGAN model files are stored after downloading.

Notes::
The provided ESRGAN model is an example. You may explore other models for better performance on your specific task.
Consider using smaller video clips for testing due to potential GPU memory constraints in Colab.
Respect copyright and licensing when working with videos.


Open Video Capture:

cap = cv2.VideoCapture(input_path)

# This line initializes a video capture object using OpenCV's VideoCapture class, which is used to read frames from the input video file specified by input_path.

Get Video Properties:

width = int(cap.get(3))
height = int(cap.get(4))
fps = cap.get(5)
# These lines retrieve the width, height, and frames per second (fps) information of the input video. These properties are used later in the code.

Define VideoWriter:

fourcc = cv2.VideoWriter_fourcc(*'mp4v')
out = cv2.VideoWriter(output_path, fourcc, fps, (width*4, height*4))
# These lines set up a VideoWriter object using OpenCV. It specifies the output video file path (output_path), codec (mp4v), frames per second, and the size of the output video, which is four times larger in both # width and height compared to the input video.

Video Processing Loop:

while cap.isOpened():
    ret, frame = cap.read()
    if not ret:
        break
# This loop reads frames from the input video until there are no more frames (cap.isOpened() checks if the video capture is still open). If ret is False, it means there are no more frames, and the loop breaks.

Preprocess Frame:

preprocessed_frame = cv2.resize(frame, (0, 0), fx=0.25, fy=0.25)
The current frame is resized to a smaller resolution (0.25 times the original size) for faster processing.

Upscale Using ESRGAN:
e
upscaled_frame = esrgan_model.predict(np.expand_dims(preprocessed_frame, axis=0))[0]
# The preprocessed frame is passed through an ESRGAN model (esrgan_model) to enhance its resolution.

Post-process Frame:

final_frame = cv2.resize(upscaled_frame, (width*4, height*4))
# The upscaled frame is resized back to the original size.

Display or Save Enhanced Frame:

out.write(final_frame)
# The final enhanced frame is written to the output video file.

Release Resources:

cap.release()
out.release()
cv2.destroyAllWindows()
# The video capture and video writer objects are released, and any OpenCV windows are closed.

Example Usage:

input_video_path = '/content/test1.mp4'
output_video_path = '/content/sample_data'
enhance_video(input_video_path, output_video_path)
# This demonstrates how to use the enhance_video function with a specific input video file (test1.mp4) and output video file path (sample_data). Note that the output file path should include the desired file extension (e.g., '.mp4').
