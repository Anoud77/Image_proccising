# Image Processing with OpenCV

This Python code performs several image processing tasks using the OpenCV (`cv2`) and scikit-image (`skimage`) libraries.  The tasks include foreground segmentation, background color replacement, contrast stretching, image sharpening, and brightness enhancement.

## Features

* **Foreground Segmentation:** Uses the GrabCut algorithm to extract the foreground from an image.
* **Background Color Replacement:** Replaces the background of an image with white.
* **Contrast Stretching:** Enhances the contrast of an image, particularly useful for dark images.
* **Image Sharpening:** Applies a sharpening filter to enhance edges and details.
* **Brightness Enhancement:** Adjusts the brightness of an image using gamma correction.

## Libraries Used

* **cv2 (OpenCV):** For image loading, color space conversion, GrabCut, and filtering.
* **numpy:** For numerical operations, especially for image data representation.
* **matplotlib.pyplot:** For displaying images and histograms.
* **skimage.exposure:** For gamma correction (brightness adjustment).

## Code Explanation

The code is organized into several sections, each performing a specific image processing task:

1.  **Foreground Segmentation:**
    * Loads an image using `cv2.imread()`.
    * Defines a rectangle (`rect`) that roughly bounds the foreground object.
    * Creates a mask to differentiate between background, foreground, and unknown pixels.
    * Applies the GrabCut algorithm (`cv2.grabCut()`) to refine the segmentation.  The algorithm iteratively estimates the foreground and background.
    * Creates a final mask where foreground pixels are marked as 1.
    * Extracts the foreground using the mask.
    * Displays the original image and the segmented foreground using `matplotlib.pyplot`.

2.  **Background Color Replacement:**
    * Defines the new background color as white (255, 255, 255) in BGR format.
    * Creates a boolean mask (`background_mask`) that identifies pixels where all color channels are zero (black pixels, which represent the removed background).
    * Replaces the black pixels in the foreground image with the new background color.
    * Displays the image with the changed background.

3.  **Contrast Stretching:**
    * Loads a dark image.
    * Optionally, the image is darkened (the provided code just assigns the original image).
    * Converts the image to grayscale using `cv2.cvtColor()`.  (The code appears to perform contrast stretching on the color image, not the grayscale version).
    * Applies contrast stretching to each color channel independently:
        * Calculates the minimum and maximum intensity values for each channel.
        * Rescales the pixel intensities to the full range of 0 to 255.
    * Converts the resulting image data to `uint8` format.
    * Displays the original image and the contrast-stretched image, along with their histograms.

4.  **Image Sharpening:**
    * Loads an image.
    * Applies a sharpening filter using `cv2.filter2D()` with a predefined sharpening kernel:
        ```
        [[-1, -1, -1],
         [-1,  9, -1],
         [-1, -1, -1]]
        ```
        This kernel emphasizes the differences between a pixel and its neighbors, thus enhancing edges and details.
    * Displays the original and sharpened images.  The original image in this section is actually the contrast-stretched image from the previous section, which might not be the intended behavior.

5.  **Brightness Enhancement:**
    * Applies Unsharp Masking (using `cv2.GaussianBlur()` and `cv2.addWeighted()`) to enhance clarity.  This technique sharpens the image by subtracting a blurred version of the image from the original.
    * Adjusts the brightness of the sharpened image using gamma correction with `skimage.exposure.adjust_gamma()`.  Gamma correction brightens the image by increasing the intensity of the pixel values.
    * Displays the sharpened image and the final brightened image.

## Usage

1.  **Prerequisites:**
    * Python 3.x
    * cv2 (OpenCV)
    * numpy
    * matplotlib
    * skimage

2.  **Installation:**

    Install the required libraries:

    ```bash
    pip install opencv-python numpy matplotlib scikit-image
    ```

3.  **Running the Code:**

    * Save the Python code to a file (e.g., `image_processing.py`).
    * Ensure that the image files specified in the code (`figimagepro7.jpg`, `figimagepro11.jpg`, and `figimagepro3.jpg`) are in the correct locations.  You may need to adjust the `image_path` variables in the code to point to the correct file paths on your system.
    * Run the script:

    ```bash
    python image_processing.py
    ```

4.  **Output:**

    The script will display several figures, each showing the results of a specific image processing step:

    * Original image and segmented foreground.
    * Foreground with the background changed to white.
    * Original image, original image histogram, contrast-stretched image, and contrast-stretched image histogram.
    * Original image and sharpened image.
    * Original image and enhanced (sharpened) image.
    * Enhanced image and brightened image
