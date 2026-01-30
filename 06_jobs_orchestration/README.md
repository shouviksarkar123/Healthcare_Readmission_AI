# Databricks Job – Patient Readmission Pipeline

# This folder documents the orchestration layer of the project.

# ## How orchestration is done
# - Using Databricks Workflows (Jobs UI)
# - Each task is a notebook
# - Dependencies follow Bronze -> Silver -> Gold -> ML

# ## Tasks
# - bronze_ingestion
# - silver_transformation
# - gold_features
# - ml_training

# ## Notes
# - No orchestration logic is hard-coded
# - UI-based workflow ensures monitoring and retry support
