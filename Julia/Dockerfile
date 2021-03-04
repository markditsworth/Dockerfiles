FROM julia:latest

# for networks
RUN julia -e 'import Pkg; Pkg.add("LightGraphs"); Pkg.add("GraphIO"); Pkg.add("SimpleWeightedGraphs");'

# for statistics
RUN julia -e 'import Pkg; Pkg.add("Distributions");'

# for plotting
RUN julia -e 'import Pkg; Pkg.add("Plots");'

# for IO
RUN julia -e 'import Pkg; Pkg.add("CSV"); Pkg.add("DataFrames");'

# for working on CommunityDetection.jl
RUN julia -e 'import Pkg; Pkg.add("Clustering"); Pkg.add("ArnoldiMethod");'
