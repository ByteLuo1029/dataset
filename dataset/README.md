# Project Overview

This folder contains all data used in the experimental part of LogSage.

## `experiment_dataset`

This folder contains datasets for baseline and ablation experiments. It includes log data from multiple projects. The directory structure of a sample project is shown below:

```
experiment_dataset/AdminLTE/
├── pair_1/
│   ├── fail/
│   │   ├── label.json
│   │   ├── content.txt
│   │   ├── template.txt
│   │   ├── fail.txt
│   │   └── fail/
│   │       ├── 1_Set_up_job.txt
│   │       ├── 1_Set_up_job_content.txt
│   │       ├── 1_Set_up_job_template.txt
│   │       ├── 2_Create_job_directory.txt
│   │       ├── 2_Create_job_directory_content.txt
│   │       ├── 2_Create_job_directory_template.txt
│   │       ├── ...
│   │       ├── label_3_Run_Dependabot.txt
│   │       ├── label_3_Run_Dependabot_content.txt
│   │       └── label_3_Run_Dependabot_template.txt
│   ├── success/
│   │   ├── success.txt
│   │   └── success/
│   │       ├── 1_Set_up_job.txt
│   │       ├── 2_Create_job_directory.txt
│   │       ├── 3_Run_Dependabot.txt
│   │       └── ...
│   └── fail_13775893480_failure_info.json
├── pair_2/
└── ...
```

Notes:

* Each project may contain one or more `pair_x` subfolders, each representing a test case. Each case includes one failed log and related data (under `fail/`) and the corresponding successful log and related data (under `success/`).
* Logs in both `fail` and `success` folders are divided into two types: complete logs and step-wise logs. Files under `fail/fail/` and `success/success/` are step-wise logs, while `fail/fail.txt` and `success/success.txt` are the complete logs. The complete logs are the concatenation of the step-wise logs.
* Each step-wise log file under the `fail` folder has three versions: the original version (e.g., `fail.txt` or files that do not end with `_template.txt` or `_content.txt`), the template version (e.g., `template.txt` or files ending with `_template.txt`), and the content version (e.g., `content.txt` or files ending with `_content.txt`). In contrast, logs under `success` only have the original version. Both the template and content versions are generated from the original version using the Drain3 parser. You should choose the appropriate version according to your experiment's requirements.
* In the step-wise logs under the `fail` folder, files prefixed with `label_` contain key information related to the failure.
* The `label.json` file in the `fail` folder is a JSON object recording the start and end line numbers of the abnormal segment, in the format: `{"start": 522, "end": 1346}`.

## `train_Drain3_dataset`

This folder contains the logs used to train the Drain3 log template extractor. For each project, the earliest log pair is selected to avoid data leakage. Structurally, this dataset does not contain the template and content versions, as those need to be generated from the original logs using Drain3.
