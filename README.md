pip install pygraphviz
import pygraphviz as pgv

# Create a new directed graph
G = pgv.AGraph(strict=False, directed=True)

# Add nodes for each layer/component of the ViT model
layers = [
    "Input Image (224x224x3)",
    "Image Patching",
    "Patch Embeddings",
    "Positional Encodings",
    "Transformer Encoder Layers",
    "Multi-Head Self-Attention",
    "Feedforward Neural Network",
    "Layer Normalization and Residual Connections",
    "Global Average Pooling",
    "Fully Connected Layer",
    "Softmax Activation",
    "Output (14 classes)"
]
for layer in layers:
    G.add_node(layer, color='lightblue', style='filled')

# Add edges to connect the layers
edges = [
    ("Input Image (224x224x3)", "Image Patching"),
    ("Image Patching", "Patch Embeddings"),
    ("Patch Embeddings", "Positional Encodings"),
    ("Positional Encodings", "Transformer Encoder Layers"),
    ("Transformer Encoder Layers", "Multi-Head Self-Attention"),
    ("Multi-Head Self-Attention", "Feedforward Neural Network"),
    ("Feedforward Neural Network", "Layer Normalization and Residual Connections"),
    ("Layer Normalization and Residual Connections", "Transformer Encoder Layers"),
    ("Transformer Encoder Layers", "Global Average Pooling"),
    ("Global Average Pooling", "Fully Connected Layer"),
    ("Fully Connected Layer", "Softmax Activation"),
    ("Softmax Activation", "Output (14 classes)")
]
for edge in edges:
    G.add_edge(*edge)

# Save the graph as an image file
G.draw('vit_model.png', prog='dot')

