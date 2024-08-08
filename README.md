# Mentor-Mentee Allocation

## Introduction

An algorithm for mentor-mentee allocation that leverages cosine similarity for matching based on shared interests and employs constraint satisfaction techniques to ensure balanced gender distribution. Developed to facilitate optimal pairing for incoming Bachelor of Science students at École Polytechnique. The mentors are the students from a promotion higher than the incoming promotion/batch (for example, the incoming BX27 students would have a BX26 student as their mentor! Each mentor (any senior student who willingy volunteers) to be one has around 4 to 5 mentees usually (or the Size of the incoming promotion/no of mentors approximately)! 

The code for the algorithm also includes data cleaning steps to handle any missing values by replacing them with empty strings. This ensures that the dataset is complete and the algorithm functions correctly.
You would find attached a pdf of the form that was sent out to the incoming Bachelor students to fill out for matching them with their mentors!
And since the official data obviously needs to remain confidential, please find a file by the name of 'Sample-Data.xlsx' in the main branch of this repository for your reference as to how you wish to handle the data and the column labels in exactly the same way as me! Else, feel free to play around!

Also Please note that you would find older yet less efficient (and possibly incomplete/not totally accurate) versions of the algorithm in the 'Develpment Phase' Branch of this repository. If you are using this repo to contribute to an open source project or anything permissible under the MIT License (see [LICENSE](https://github.com/JaiAnshSB26/Mentor-Mentee-Allocation-Algorithm/blob/main/LICENSE)), feel free to play around with the code a bit to get the best optimized version for your data, since that is exactly what I did.

**NB:-** We used the same form for the mentors and the mentees, and since the majority of the mentees (the incoming promtion) didn't have access to their institutional email id s yet, and the mentors (the second year students for the academic year 2024 - 25) did, I used this as a factor to separate out the mentors from the mentees, instead of sorting them out by hand in the excel sheet (extracted from the responses collected from the form). So to do that, when some of the mentees who filled the form after recieving their institutional email id s, I assigned random domain names to their email addresses to avoid cleaning all the data to eparate out the mentors and mentees. You might need to handle a very different set of data (or an extracted spreadsheet), so you can definitely think of other ways to separate out the mentors and the mentees!

## Requirements
- Python 3.x (any higher version!)
- Pandas
- NumPy
- scikit-learn
- OpenPyXL (for Excel file handling)

Please note that I have uploaded the code in the form of a Jupyter Notebook here, as it is easier to show live output and explain concepts using text cells, rather than leaving comments for everything in a Python file. You will have the same requirements for the Jupyter Notebook (if you decide to run the code/algorithm in Jupyter Notebook itself). You can run the pip install commands in your Jupyter (or Anaconda if you are accessing it from there) notebook-specific environment or the command window (if you don't have these installed in your system/environment and there is an error message when you try to import modules).

## Setup

1. Install the required Python packages:

    ```bash
    pip install pandas numpy scikit-learn openpyxl
    ```

2. Place the input Excel file containing the form responses in the specified directory.

## Input File

The input Excel file should contain responses from both mentors and mentees. The file should have the following columns:

- Full name
- Email
- Hobbies (3 choice max)
- What genre of music do you like?
- What would you like to do in Paris
- Regarding the previous question, any plans/ideas in particular?
- Gender

Mentors should have email addresses containing `@polytechnique.edu`. Mentees should have non-polytechnique email addresses.

## Algorithm Description

The algorithm uses the following steps to allocate mentees to mentors:

### 1. Data Loading and Cleaning

The algorithm starts by loading the Excel file and filling any missing values with empty strings to ensure there are no gaps in the data.

### 2. Separation of Mentors and Mentees

Mentors and mentees are separated based on their email addresses. Mentors have `@polytechnique.edu` email addresses, while mentees have non-polytechnique email addresses.

### 3. Gender Information Check

The script checks to ensure that gender information is available for both mentors and mentees. If the gender information is missing, the script raises an error.

### 4. Combining Interests

The script combines the various interest columns (hobbies, music preferences, activities in Paris, and plans/ideas) into a single string for each mentor and mentee. This combined string is used for similarity calculation.

### 5. Similarity Calculation

The script uses the cosine similarity measure to calculate the similarity between mentors and mentees based on their combined interests. Cosine similarity is a measure of similarity between two non-zero vectors that calculates the cosine of the angle between them.

### 6. Sorting and Allocation

Mentees are sorted by their similarity scores to mentors. The script then allocates mentees to mentors in a round-robin fashion while ensuring balanced gender distribution among mentees in each group. The script ensures that each mentor receives a roughly equal number of mentees by considering the capacity and gender constraints.

### 7. Creating and Saving Allocation DataFrame

The final mentor-mentee allocations are formatted into a DataFrame and saved to an Excel file named `Mentor_Mentee_Allocation.xlsx`.

## Running the Script

1. Modify the file path in the script to point to your input Excel file.
2. Run the script:

    ```bash
    python mentor_mentee_allocation.py
    ```

3. The script will generate an output Excel file named `Mentor_Mentee_Allocation.xlsx` in the specified directory containing the mentor-mentee allocations.

## Output File

The output Excel file will contain two columns:
- Mentor: The name of the mentor.
- Mentee: The name of the allocated mentee.
