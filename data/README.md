# Dataset Preparation

This directory defines the runtime dataset layout expected by the released D-NSGA2+ C++ implementation.

Large benchmark CSV files are maintained in the separate public dataset repository:

```bash
git clone https://github.com/IOAS-HQU/DataSet.git
```

This code repository tracks only the folder skeleton, `.gitkeep` placeholders, and task-list templates. Copy the required CSV files from the dataset repository into the target layout below before running the executable.

## Target Layout

```text
data/
|-- realworld_45/
|   |-- data/
|   |   |-- Mytxt.txt
|   |   `-- processed/
|   `-- time-distance-matrix/
|       |-- src-src-time/
|       |-- dest-dest-time/
|       |-- dest-src-time/
|       |-- src-dest-time/
|       |-- src-src-dis/
|       |-- dest-dest-dis/
|       |-- dest-src-dis/
|       `-- src-dest-dis/
`-- solomon_36/
    |-- data/
    |   |-- Mytxt.txt
    |   |-- c/
    |   |-- r/
    |   `-- rc/
    `-- time-distance-matrix/
```

## Required Files

### Real-world 45 instances

Copy the real-world instance files from the dataset repository into these target folders:

```text
<dataset-repo>/.../xiamen_zhangzhou_45/data/processed/*.csv
  -> data/realworld_45/data/processed/

<dataset-repo>/.../xiamen_zhangzhou_45/time-distance-matrix/src-src-time/*.csv
  -> data/realworld_45/time-distance-matrix/src-src-time/

<dataset-repo>/.../xiamen_zhangzhou_45/time-distance-matrix/dest-dest-time/*.csv
  -> data/realworld_45/time-distance-matrix/dest-dest-time/

<dataset-repo>/.../xiamen_zhangzhou_45/time-distance-matrix/dest-src-time/*.csv
  -> data/realworld_45/time-distance-matrix/dest-src-time/

<dataset-repo>/.../xiamen_zhangzhou_45/time-distance-matrix/src-dest-time/*.csv
  -> data/realworld_45/time-distance-matrix/src-dest-time/

<dataset-repo>/.../xiamen_zhangzhou_45/time-distance-matrix/src-src-dis/*.csv
  -> data/realworld_45/time-distance-matrix/src-src-dis/

<dataset-repo>/.../xiamen_zhangzhou_45/time-distance-matrix/dest-dest-dis/*.csv
  -> data/realworld_45/time-distance-matrix/dest-dest-dis/

<dataset-repo>/.../xiamen_zhangzhou_45/time-distance-matrix/dest-src-dis/*.csv
  -> data/realworld_45/time-distance-matrix/dest-src-dis/

<dataset-repo>/.../xiamen_zhangzhou_45/time-distance-matrix/src-dest-dis/*.csv
  -> data/realworld_45/time-distance-matrix/src-dest-dis/
```

Use the task list tracked in this repository:

```text
data/realworld_45/data/Mytxt.txt
```

### Modified Solomon 36 instances

Copy the Solomon instance files from the dataset repository into these target folders:

```text
<dataset-repo>/.../modified_solomon_36/data/c/*.csv
  -> data/solomon_36/data/c/

<dataset-repo>/.../modified_solomon_36/data/r/*.csv
  -> data/solomon_36/data/r/

<dataset-repo>/.../modified_solomon_36/data/rc/*.csv
  -> data/solomon_36/data/rc/

<dataset-repo>/.../modified_solomon_36/time-distance-matrix/*.csv
  -> data/solomon_36/time-distance-matrix/
```

Use the task list tracked in this repository:

```text
data/solomon_36/data/Mytxt.txt
```

## Task-List Formats

`data/realworld_45/data/Mytxt.txt` uses the full 11-column format:

```text
stoptime max_delay data_file time1 time2 time3 time4 dist1 dist2 dist3 dist4
```

`data/solomon_36/data/Mytxt.txt` uses the concise 6-column format:

```text
stoptime data_file time1 time2 time3 time4
```

For the Solomon format, the code uses `EXPERIMENT_DEFAULT_MAX_DELAY` and reuses the four time matrices as distance matrices, matching the historical Solomon experimental setup.

## Choosing a Dataset

By default, the loader follows `ExperimentConfig.h`.

To run the real-world 45-task group, use:

```cpp
const char* const EXPERIMENT_TASK_LIST_PATH = "data/realworld_45/data/Mytxt.txt";
const int EXPERIMENT_TASK_END = 45;
```

To run the modified Solomon 36-task group, use:

```cpp
const char* const EXPERIMENT_TASK_LIST_PATH = "data/solomon_36/data/Mytxt.txt";
const int EXPERIMENT_TASK_END = 36;
```

Generated outputs are written to `Result/` and `Stage/`, which are ignored by Git.
