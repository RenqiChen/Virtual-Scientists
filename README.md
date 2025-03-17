# README

<div align="center"><img src=".gitbook/assets/logo.png" alt="" width="700"></div>

## Many Heads Are Better Than One: Improved Scientific Idea Generation by A LLM-Based Multi-Agent System.

### 👀 Introduction

This repository contains the code for our paper `Many Heads Are Better Than One: Improved Scientific Idea Generation by A LLM-Based Multi-Agent System`.

* To the best of our knowledge, we propose the first multi-agent system with a scientific research ecosystem for conducting and benchmarking scientific collaborations, named VirSci, where real data is used for role-playing and objective evaluation.
* To simulate a reliable scientific collaboration process, we propose an end-to-end pipeline that spans team organization to idea generation. A novel inter- and intra-team discussion mechanism is introduced to promote communication topology and enhance the simulation realism.
* Extensive experiments demonstrate that multi-agent collaboration improves outcome quality, surpassing existing methods. We also conduct systematic experiments to investigate factors influencing the system, with findings aligning with established principles from the Science of Science, such as fresh teams tend to generate more innovative research, underscoring VirSci's reliability as a powerful tool for autonomous scientific discovery.

Our project website is [Website](https://renqichen.github.io/Virtual-Scientists/).

### 📆 Updates

#### \[2025-02]

1. We update our paper with Appendix on [Arxiv](https://arxiv.org/pdf/2410.09403).

#### \[2024-10]

1. We propose the VirSci, a multi-agent system has the potential to improve scientific idea generation.
2. Watch demo video for our project at [YouTube](https://www.youtube.com/watch?v=p_Vdpq8ImeE).
3. Full paper with Appendix is available on [Arxiv](https://arxiv.org/abs/2410.09403).
4. VirSci code and data are available for Research community.

### 💡 Run

#### Environment

We tested our codebase with PyTorch 2.3.1 and CUDA 12.1. Please install the corresponding versions of PyTorch and CUDA based on your computational resources.

To install the required packages, run:

```bash
pip install -r requirements.txt
```

**Note**

If you encounter any errors while setting up the environment, do not panic, as our environment is deployed on the ARM architecture, which may cause some package versions to be unavailable. The most important thing is to install agentscope in `editable mode` 😀, which can be easily installed using the command:

```
cd agentscope-main
pip install -e .
```

Another kind advice is that our code uses `faiss` during execution, and we highly recommend installing `faiss-gpu`.

#### Setup

The raw data is based on the [AMiner Computer Science Dataset](https://www.aminer.cn/aminernetwork).

After preprocessing, the used data is publicly available at [Google Drive](https://drive.google.com/drive/folders/1ZwWMBQ5oK-l4VuzMa60GbMND0g2EIxIu?usp=sharing).

* Past paper database is put in the `Papers/papers.tar.gz`, which is used in `paper_folder_path` of Line 34 in `sci_platform/sci_platform.py`. The corresponding embedding database is put in the `Embeddings/faiss_index.index`, which is used in `cpu_index` of Line 135 in `sci_platform/sci_platform.py`.
* Contemporary paper database is put in the `Papers/papers_future.tar.gz`, which is used in `future_paper_folder_path` of Line 35 in `sci_platform/sci_platform.py`. The corresponding embedding database is put in the `Embeddings/faiss_index_future.index`, which is used in `cpu_future_index` of Line 139 in `sci_platform/sci_platform.py`.
* Author knowledge bank is put in the `Authors/books.tar`, which is used in in `input_dir` of Line 13 in `sci_platform/configs/knowledge_config.json` and `author_info_dir` of Line 36 in `sci_platform/sci_platform.py`.
* Adjacency matrix is put in the `adjacency.txt`, which is used in `adjacency_matrix_dir` of Line 37 in `sci_platform/sci_platform.py`.

**Note**

Please replace all paths in `sci_platform/sci_platform.py` with your own settings after download the data.

#### Code

Here we explain the roles of several critial files.

* `agentscope-main/src/agentscope/agents/sci_agent.py` defines the customized scientist agent in this project.
* `sci_platform/run.py` is the main execution file.
* `sci_platform/sci_platform.py` defines the platform for the initialization of our multi-agent system.
* `sci_platform/utils/prompt.py` contains all the prompts used.
* `sci_platform/utils/scientist_utils.py` contains all the common functions used.
* `sci_platform/sci_team/SciTeam.py` defines the execution mechanism of each scientist team.

#### Usage

**Ollama**

In our experiments, we use `ollama` to deploy the `llama3.1-8b` and `llama3.1-70b` language models and `mxbai-embed-large` embedding model. The details of deployment could refer to [URL](https://github.com/ollama/ollama-python). Here we show some key steps:

1. Ollama should be installed. The linux version:

```
curl -fsSL https://ollama.com/install.sh | sh
```

2. Run ollama in the path where ollama is installed:

```
./ollama serve
```

3. Pull a model to use with the library:

```
./ollama pull llama3.1
./ollama pull llama3.1:70b
./ollama pull mxbai-embed-large
```

4. Install the ollama python library in your environment:

```
pip install ollama
```

5. Complete the installation and close the terminal.

**Run**

After pull all models, you need to open the ollama server before running our codes:

```
./ollama serve
```

Then, run our codes:

```
cd sci_platform/
python run.py
```

Our code support different collaboration settings. The commonly used arguments:

`--runs`: how many times does the program run

`--team_limit`: the max number of teams for a scientist

`--max_discuss_iteration`: the max discussion iterations for a team in a step

`--max_team_member`: the max team member of a team (including the team leader)

`--epochs`: the allowed time steps for one program run (default value is 6, which is enough for a scientist to finish all steps)

#### Results

* `{info_dir}/{current_time}_{self.team_name}_dialogue.json` saves the team information: **all team members, selected topic, generated idea and abstract**, where `info_dir` denotes the storage path, `current_time` denotes the start running time, and `self.team_name` is the name of the team.
* `{log_dir}/{current_time}_{self.team_name}_dialogue.log` saves the log record of the team, where `log_dir` denotes the storage path.

### 🙏 Acknowledgements

This project is supported by Shanghai Artificial Intelligence Laboratory.

The multi-agent framework in this work is based on the [AgentScope](https://github.com/modelscope/agentscope).

The raw data is based on the [AMiner Computer Science Dataset](https://www.aminer.cn/aminernetwork).

### 📧 Contact

If you have any questions, please contact at \[chenrenqi@pjlab.org.cn, suhaoyang@pjlab.org.cn].

Welcome to join our discussion group on collective intelligence technology!

| Wechat                         |
| ------------------------------ |
| ![](.gitbook/assets/Group.jpg) |

#### Note

If you find that the WeChat QR code has expired, please send us an email with your WeChat ID, and we will manually invite you to the group.

### ⚖ License

This repository is licensed under the [Apache-2.0 License](LICENSE/).

### 📌 BibTeX & Citation

If you find this code useful, please consider citing our work:

```bibtex
@misc{su2025headsbetteroneimproved,
      title={Many Heads Are Better Than One: Improved Scientific Idea Generation by A LLM-Based Multi-Agent System}, 
      author={Haoyang Su and Renqi Chen and Shixiang Tang and Zhenfei Yin and Xinzhe Zheng and Jinzhe Li and Biqing Qi and Qi Wu and Hui Li and Wanli Ouyang and Philip Torr and Bowen Zhou and Nanqing Dong},
      year={2025},
      eprint={2410.09403},
      archivePrefix={arXiv},
      primaryClass={cs.AI},
      url={https://arxiv.org/abs/2410.09403}, 
}
```
