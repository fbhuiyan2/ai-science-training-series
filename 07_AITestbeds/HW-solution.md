# Theory Homework Solutions

1. **What are the key architectural features that make these systems suitable for AI workloads?**
   The key architectural features that make AI accelerators like SambaNova, Cerebras, Graphcore, and Groq systems suitable for AI workloads are:
   1. Specialized Hardware Design to accelerate matrix multiplications and tensor operations.
   2. High Memory Bandwidth and larger amount of on-chip memory help to accelerate memory intensive AI worklaods. 
   3. Scalability and Parallelism: Parallel processing of data across many cores or processing units, which significantly speeds up training and inference tasks


2. **Identify the primary differences between these AI accelerator systems in terms of their architecture and programming models.**
   
    1.  Sambanovas Reconfigurable Dataflow Unit (RDU) allows for flexible dataflow processing that features a multi-tiered memory architecture with terabytes of addressable memory for efficinet handling of large data. 
    2.  Cerebras Wafer-Scale Engine (WSE) consists of processing elements (PEs) with its own memory and operates independently. Fine-grained dataflow control mechanism within its PEs make the system highly parallel and scalable.
    3. Graphcore’s Intelligence Processing Unit (IPU) consists of many interconnected processing tiles, each with its own core and local memory. The IPU operates in two phases—computation and communication—using Bulk Synchronous Parallelism (BSP).
    4. Groq’s Tensor Streaming Processor (TSP) architecture focuses on deterministic execution which s particularly advantageous for inference tasks where low latency is critical.


3. **Based on hands-on sessions, describe a typical workflow for refactoring an AI model to run on one of ALCF's AI testbeds (e.g., SambaNova or Cerebras). What tools or software stacks are typically used in this process?**

    Typical worksflow involves using vendor specific implementation of ML framework like PyTorch to port model. Let's think about PyTorch models here.

    ### Typical Workflow for Refactoring PyTorch Models

    - Step 1: Profile the Existing PyTorch Model
      - Evaluate Model Components: Identify custom layers, operations, and data types.
      - Benchmark Performance: Establish baseline performance metrics for later comparison.
      - Dependency Analysis: Check for dependencies that may not be supported on the target platform.
    - Step 2: Understand the Target Hardware Architecture
      - Read Documentation: Familiarize yourself with the hardware capabilities and limitations.
      - Consult Examples: Review sample models and code provided by SambaNova and Cerebras.
      - Identify Supported Features: Note which PyTorch features are fully supported, partially supported, or unsupported.
    - Step 3: Modify the Model for Compatibility
      - Replace Unsupported Operations: Substitute or re-implement layers that are incompatible.
      - Optimize Data Structures: Adapt data loading and preprocessing to match the hardware's requirements.
      - Adjust Hyperparameters: Modify training parameters to suit the new environment.


### Tools and Software Stacks Used

Let's take Sambanova for example. 

### SambaNova Software Stack
- **SambaFlow SDK**

**Description:** SambaFlow is the primary SDK for developing and running models on SambaNova hardware.

**Features:**

  - Compiler that transforms PyTorch models for execution on RDA.
  - Tools for model optimization and profiling.
  - APIs for integrating custom operations.

- **PyTorch Integration**
  
**Approach:**

  - Use SambaFlow's PyTorch frontend to write models.
  - Annotate code where necessary to guide the compiler.
  - Leverage SambaNova-specific libraries for additional functionalities.
