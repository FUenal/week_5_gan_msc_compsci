-----

# Monet-Style Painting Generation with CycleGANs

**Author:** Fatih Uenal  
**Course:** CU Boulder MSc Computer Science & AI  
**Kaggle Competition:** [I’m Something of a Painter Myself](https://www.kaggle.com/competitions/gan-getting-started)

## Project Overview

This project explores the fascinating intersection of artificial intelligence and art by using a Generative Adversarial Network (GAN) to perform artistic style transfer. The primary goal is to build and train a model capable of transforming real-world photographs into beautiful paintings in the distinct, impressionistic style of Claude Monet.

The project was developed as part of the "I’m Something of a Painter Myself" Kaggle competition, using an enhanced CycleGAN architecture optimized for high-quality, textured image generation on a TPU.

## Final Results

The final model successfully learns to apply Monet's style, including characteristic brushstrokes and color palettes, to input photographs.

#### Sample Generated Image
![sample image](sample.png)

#### Final Score (MiFID)

*(Please replace this line with a screenshot of your final score)*
![My Score](score_image.png)

#### Leaderboard Position

*(Please replace this line with a screenshot of your leaderboard position)*
![My Leaderboard Position](leaderboard_image.png)

## Technical Approach

While the foundational model is a CycleGAN, a standard implementation was found to be insufficient for producing high-fidelity, textured results. This project implements a professional-grade, enhanced CycleGAN incorporating several state-of-the-art techniques:

  * **CycleGAN Architecture:** A robust dual-generator/dual-discriminator setup with a **U-Net based Generator**, whose skip connections are crucial for preserving the content of the original photo.
  * **Perceptual Loss (VGG19):** A key component for achieving a realistic "painterly" feel. By comparing feature maps from a pre-trained VGG19 network, this loss function forces the generator to learn and replicate high-level stylistic features like texture and brushstrokes, not just color.
  * **Data Augmentation:** Random resizing, cropping (jitter), and horizontal flipping were applied during training. This makes the discriminator's task more challenging, compelling the generator to create more convincing and detailed images.
  * **Custom Learning Rate Scheduler:** A `LinearDecay` scheduler was implemented to ensure training stability. The learning rate is kept constant for the first half of the epochs for rapid progress and then linearly decayed to zero, allowing the model to refine fine-grained details in the later stages.
  * **TPU-Optimized Training:** The entire training pipeline is designed for efficient, distributed training on a Tensor Processing Unit (TPU), utilizing a manual training loop with `strategy.run()` for maximum performance and stability.

## Dataset

This project uses the `gan-getting-started` dataset provided by Kaggle, which contains two sets of images in TFRecord format:

  * A collection of Claude Monet's paintings.
  * A large set of real-world photographs intended for style transfer.

## How to Run

The entire project is contained within the provided Kaggle notebook (`week-5-gan-msc-compsci.ipynb`).

1.  **Environment:** The notebook is designed to be run in a Kaggle environment with a **TPU v3-8 accelerator** enabled.
2.  **Data:** The competition dataset will be automatically attached when you open the notebook in Kaggle.
3.  **Execution:** Simply run all the cells in the notebook from top to bottom. The script will handle data loading, model training, and finally, the generation of a `images.zip` file for submission.

Key dependencies include `tensorflow`, `numpy`, and `matplotlib`.

## Conclusion and Future Work

This project successfully demonstrates the power of advanced GAN techniques to achieve high-quality artistic style transfer. The final model is capable of producing compelling, textured images that convincingly mimic the style of Claude Monet.

For a detailed discussion of potential next steps and further improvements, please see the **"Future Work"** section at the end of the project notebook. Key ideas include experimenting with a ResNet-based generator and further hyperparameter tuning.

---

## Acknowledgments

* Kaggle and the organizers for providing a rich, real-world dataset.
* The MSc Computer Science & AI program for framing this as a hands-on assignment.

---
