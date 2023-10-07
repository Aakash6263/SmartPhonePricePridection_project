# Smartphone Price Prediction Project

## Introduction

Smartphones are integral to modern life, serving various purposes. Predicting smartphone prices is crucial for consumers, manufacturers, and retailers. This project aims to develop a machine learning model to predict smartphone prices, which will aid consumers in making cost-effective choices and help manufacturers and retailers in setting competitive prices and strategic stocking.

## Data Overview

The dataset used for this project contains the following columns:

- `brand_name`: The name of the smartphone's manufacturer or brand.
- `model`: The specific model or name of the smartphone.
- `price`: The price of the smartphone.
- `rating`: The user or expert rating of the smartphone.
- `has_5g`: A boolean (True/False) indicating whether the smartphone has 5G connectivity capabilities.
- `has_nfc`: A boolean indicating whether the smartphone has Near Field Communication (NFC) technology.
- `has_ir_blaster`: A boolean indicating whether the smartphone has an Infrared (IR) blaster, which can be used as a remote control.
- `processor_brand`: The brand or manufacturer of the smartphone's processor.
- `processor_name`: The specific name or model of the smartphone's processor.
- `num_cores`: The number of processing cores in the smartphone's CPU.
- `processor_speed`: The clock speed or processing speed of the smartphone's CPU.
- `os`: The operating system installed on the smartphone (e.g., Android, iOS).
- `ram_capacity_gb`: The amount of Random Access Memory (RAM) in gigabytes available in the smartphone.
- `internal_memory`: The storage capacity of the smartphone's internal memory, typically in gigabytes.
- `battery_capacity_mAh`: The capacity of the smartphone's battery, measured in milliampere-hours (mAh).
- `fast_charging`: Information about whether the smartphone supports fast charging technology.
- `has_fastcharge`: An integer value indicating fast charging capabilities.
- `screen_size`: The size of the smartphone's screen, typically in inches.
- `resolution`: The screen resolution of the smartphone.
- `refresh_rate`: The refresh rate of the smartphone's display, typically in Hertz (Hz).
- `primary_camera_rear_mp`: The megapixels of the primary (rear-facing) camera.
- `primary_camera_front_mp`: The megapixels of the primary (front-facing) camera.
- `memory_card_available`: An integer value indicating the availability of a memory card slot for expanding storage.
- `extended_memory_gb`: The maximum capacity for extended memory using a memory card, typically in gigabytes.
- `total_cameras`: The total number of cameras (front and rear) in the smartphone.

## Data Gathering
We collect the data using web scraping.
### Data Collection

We employed Selenium to automate the process of gathering HTML data from the Smartprix website. This included navigating through the site, selecting checkboxes, and executing actions to load a comprehensive dataset.

### Data Storage

The collected HTML data was saved to an HTML file for further processing.

### Data Extraction

We employed BeautifulSoup and the requests module to parse the saved HTML file, extract valuable information, and transform it into a structured DataFrame for analysis.

## Data Assessment

After reviewing the scraped data, certain problems were identified.

### Quality Issues

- `model`: Some brands are written differently like OPPO & Oppo in the `model` column.
- `price`: Contains unnecessary '₹'.
- `price`: Contains ',' between numbers.
- `rating`: Missing values.
- `processor`: Some processor values are incorrect in rows (515, 528, 592, 687, 913).
- `memory (ram)`: Incorrect values in rows (51, 174, 290, 450, 517, 519, 520, 532, 541, 596, 626, 691, 719, 723, 724, 792, 851, 881, 886, 908, 917, 949, 955, 984, 994, 1004).
- `battery`: Incorrect values in rows (183, 343, 450, 519, 520, 531, 541, 596, 626, 691, 723, 724, 886, 908, 917, 949, 984, 1004).
- `display`: Sometimes frequency is not available.
- `display`: Incorrect values in rows (172, 179, 339, 515, 528, 537, 592, 687, 719, 720, 882, 913).
- Certain phones are foldable, and the info is scattered.
- `camera`: Words like Dual, Triple, and Quad are used to represent the number of cameras, and front and rear cameras are separated by '&'.
- `camera`: Problems with rows (64, 179, 181, 209, 219, 261, 277, 302, 339, 401, 408, 418, 445, 456, 458, 466, 479, 482, 483, 497, 528, 537, 557, 563, 569, 574, 584, 591, 592, 624, 643, 649, 687, 715, 719, 720, 741, 755, 758, 775, 788, 797, 798, 800, 801, 803, 805, 882, 889, 895, 907, 908, 909, 913, 957, 963, 987, 1002, 1013, 1017, 1018).
- `card`: Sometimes contains info about OS and camera.
- `os`: Sometimes contains info about Bluetooth and FM radio, etc.
- Missing values in `rating`, `card`, and `os`.

### Tidiness Issues

- `sim`: Can be split into 3 columns: `has_5g`, `has_NFC`, `has_IR_Blaster`.
- `ram`: Can be split into 2 columns: `ram_capacity_gb` and `internal_memory`.
- `processor`: Can be split into `processor_name`, `num_cores`, `processor_speed`, and `processor_brand`.
- `battery`: Can be split into `battery_capacity_mAh`, `fast_charging`, and `has_fastcharge`.
- `display`: Can be split into `screen_size`, `resolution`, and `refresh_rate`.
- `camera`: Can be split into `num_front_cameras`, `num_rear_cameras`, `primary_camera_rear_mp`, and `primary_camera_front_mp`.
- `card`: Can be split into `memory_card_available` and `extended_memory_gb`.
- `model`: Can be split into `model` and `brand_name`.

## Data Cleaning

The extracted data underwent extensive cleaning and preprocessing to handle quality and tidiness issues, including missing values, incorrect data types, and data shifting problems.

## Exploratory Data Analysis (EDA)

In the EDA phase, a thorough examination of the dataset was conducted. Data visualization techniques, including histograms, box plots, etc., were used to gain insights into feature distributions and relationships between variables. Specifically, the distribution of smartphone prices, ratings, processor speeds, battery capacities, RAM, and internal memory capacities were explored. Additionally, correlation analysis was conducted to visualize correlations between numerical features using a heatmap and pair plots.

## Feature Engineering

In the Feature Engineering phase, various techniques were employed to enhance the quality of the dataset and prepare it for machine learning models. These included handling missing data, creating new features, and one-hot encoding categorical variables.

## Machine Learning

Machine learning techniques were applied to predict smartphone prices. The dataset was split into training and test sets, and features were standardized. Four models were employed: Random Forest Regressor, Decision Tree Regressor, Support Vector Regression, and KNN Regressor. Hyperparameter tuning was performed using GridSearchCV to optimize model performance.

## Model Evaluation and Selection

To choose the best model among the options (Random Forest, Decision Tree, SVR, and KNN), various factors were considered, including the R-squared scores, potential overfitting or underfitting, and the specific requirements of the problem. Here's an analysis of each model:

### Random Forest:

- Train R-squared: 0.975
- Test R-squared: 0.911
- The Random Forest model has very high R-squared scores on both the training and test data, indicating a strong ability to fit the data. However, there is a slight performance drop from training to testing, suggesting some level of overfitting, although not severe.

### Decision Tree:

- Train R-squared: 0.905
- Test R-squared: 0.850
- The Decision Tree model has a lower R-squared score compared to Random Forest and shows a drop in performance from training to testing, indicating some overfitting.

### SVR (Support Vector Regression):

- Train R-squared: 0.937
- Test R-squared: 0.895
- SVR performs well with high R-squared scores on both training and test data. The drop in performance from training to testing is relatively small, suggesting that it may not be overfitting the data. 

### KNN (K-Nearest Neighbors):

- Train R-squared: 0.999
- Test R-squared: 0.863
- KNN has an extremely high R-squared score on the training data, but it drops significantly on the test data, indicating severe overfitting. This model may not generalize well to new, unseen data.

Based on this information, it appears that the Support Vector Regression (SVR) model is the most suitable choice for this problem. It has a good balance between high R-squared scores and minimal overfitting.

Hence, we choose Support Vector Regression (SVR).

---
