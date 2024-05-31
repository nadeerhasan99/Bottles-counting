The purpose of this algorithm is to detect and count the number of bottles present in an image of a bottle crate. The algorithm utilizes image processing techniques to isolate and identify circular objects representing bottles.
After some pre-processing operations (Geometrical and morphological) , we use Hough transform to detect two kind of circles , the small one represent the bottle cap, and the second one represent the bottle bottom (in case the bottle upside down the carte ).

Image Pre-processing:

The algorithm begins by reading the input image of the bottle crate.

If the image is in color, it is converted to grayscale for easier processing.

Top-hat transform is applied to enhance the contrast of the grayscale image, particularly emphasizing bright regions against a relatively dark background.

The enhanced grayscale image is binarized using Otsu's thresholding method to segment objects from the background.

Morphological closing operation is performed to smooth the binary image and fill in small gaps or holes within the objects.

A bounding box is defined to specify the region of interest (ROI) within the bottle crate area.

A binary mask is created based on the bounding box to isolate the ROI from the rest of the image.

The binary mask is applied to the binary image obtained from the previous step to extract the ROI.
Our pre-processing is designed to highlight important elements in the image by:

Emphasizing the circle representing the bottle cap.
Emphasizing the circle representing the bottle bottom in case of an upside-down bottle.
Avoiding pitfalls such as mistaking a plastic cup or the circular empty space in the bottle carte for the bottle cap.
Emphasizing bottle caps that are located beneath a plastic cup.




Circle Detection using Hough Transform:

Hough transform is applied to detect circular objects within the ROI.

Two separate rounds of circle detection are performed with different radius ranges :
detect the bottle cap.
detect the bottle bottom.

Detected circle centres and radii are obtained from the Hough transform.

Post-processing:

Detected circles are subjected to a post-processing step to remove or merge closely spaced circles, which may represent overlapping circles or artifacts.

A custom function merge_or_remove_circles is implemented for this purpose.

The function iterates through pairs of detected circles, calculates the distance between their centers, and compares their radii.

If the distance between two circles is below a predefined threshold, the circle with the larger radius is removed.

This step helps in eliminating false detections and ensuring accurate counting.

Counting and Visualization:

The total number of circles (representing bottles) after post-processing is counted.

Detected circles along with their counts are overlaid on the original grayscale image for visualization.

The total count is displayed as text on the image for easy interpretation.
