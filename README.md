# @bstrickl/blurriness

Utility library to help determine how blurry images are. Blurriness scores are between 0 and 1, with higher values representing images that are more blurry.

This is simply an approximation, calculated as the inverse standard deviation of the image gradient after being passed through a Sobel filter.

In other words, we are detecting edges in the image and then assuming that more edges means the image is less blurry. This assumption may not make sense in all cases.

The score itself does not mean anything without some context for what is considered "normal" for your images.

For example, in my tests images with a score of around 0.6 were very sharp while images with a score of 0.8 and above were blurry.

The best way to use these results is in conjunction with a stats library (like stats-lite) to compute the mean and standard deviation of your results in order to find which images are your outliers.

## Installation

```
npm i @bstrickl/blurriness
```

## Usage

To get the blurriness score of an image in TypeScript:

```
import { Blurriness } from '@bstrickl/blurriness';
const blurryScore: number = await Blurriness.getBlurrinessAsync('./image.jpg');
```

## Functions

**async function getBlurrinessAsync(imagePath: string): Promise\<number\>**

  Returns a blurriness score for an image between 0 and 1. Higher values are more blurry. The value returned is the inverse standard deviation of the image gradient after being passed through a Sobel filter. A higher standard deviation means that the image has more edges, with the assumption being that more edges means the image is less blurry.
