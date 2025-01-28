# Updates
# import networkx as nx
# import matplotlib.pyplot as plt

# chain_of_command = {
    "101st Three Red Arrows Brigade": {
        "Commanding Officer": "N/A",
        "Executive Officer": "N/A",
        "Division Sergeant Major": "N/A",
        "Brigades": {
            "24th Auxiliary 'Makilos'": {
                "Company Commanding Officer": "N/A",
                "Company Executive Officer": "N/A"
            },
            "36th Auxiliary 'Tagatabag'": {
                "Company Commanding Officer": "N/A",
                "Company Executive Officer": "N/A"
            }
        }
    }
}

G = nx.DiGraph()

for brigade, details in chain_of_command.items():
    G.add_node(brigade)
    for position, officer in details.items():
        G.add_node(officer)
        G.add_edge(brigade, officer)
    if "Brigades" in details:
        for brigade_name, brigade_details in details["Brigades"].items():
            G.add_node(brigade_name)
            G.add_edge(brigade, brigade_name)
            for position, officer in brigade_details.items():
                G.add_node(officer)
                G.add_edge(brigade_name, officer)

pos = nx.spring_layout(G)
nx.draw(G, pos, with_labels=True)
plt.show()
