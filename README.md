# voxel_stair_activity

## Running the Code
I would recommend stepping through the cells in the notebook file, as I was also using the notebook format while developing this solution. The `video_folder` variable will need to be updated to reflect the file path at which the video files are. (The Kaggle link to dataset is [here](https://www.kaggle.com/datasets/vincyjoel/cctv-01?resource=download).

The output of running the `batch_process` function will be a CSV file, where the columns are the name of the video file, the detected status, and the start and end timestamps of these statuses. An example output is included (stair_usage_log.csv), which was generated from applying my code to all the videos that had stairs in them.

## My Development Process/Reasoning
I chose to use a motion detection approach using differences between frames because out of some of the other ideas I had, it was the quickest to implement. I made some improvements to this approach, such as using a polygon to identify the stairs in the frame rather than a rectangle and experimenting with various parameters, like the background subtractor and the motion threshold. Additionally, the main ask that Dana was highlighting was a way to know when our stairs are actually being used vs. when they're free. I thought this approach would at least be a good initial signal for determining when stairs are idle. 

I chose to create a CSV file that shows the idle/in-use times because I thought it would be most flexible for building out a usable solution. If they wanted to, Dana's team could work directly with the CSV file or plug it into any of their existing solutions, as it's a pretty universal format of data. Another option I'm envisioning is that there is some type of logging app or dashboard app that highlights the idle times. We could ingest the CSV file into the app and create records/entities of these idle intervals. 

In terms of evaluation, the quickest idea I ended up using was to randomly choose 5 videos that were relatively short and manually check the outputted CSV results with the video footage. 

## Future Directions
Maybe it's not necessary to detect motion to define if a stair is idle or not. Instead, it could be sufficient to just detect if people are *on* the stairs, rather than is something moving on the stairs. This would make my approach more robust because people could technically stop and chat on the stairs, which would probably be classified as "idle" with my current approach. 

I also think my approach works specifically for this dataset, but later on if we add more cameras of different scenes, it could be tedious to find the polygon that defines the area of interest for each camera. Instead, maybe we could also leverage more sophisticated computer vision/object detection techniques to find the stairs in the first frame of the video. This would eliminate manually defining the polygons.

Another area that I would have liked to spend more time on is the evaluation of how well this approach is working. For the sake of time, I randomly chose 5 videos that were no longer than ~30 seconds and manually checked if the CSV output of idle/in-use intervals matched the video output. However, if I had access to ground truth labels, I would be able to more rigorously evaluate the performance of my approach. 
