
# Visualizing Neuronal Networks from SCKAN in the Open Physiology Viewer

[![N|Solid](https://images.ctfassets.net/6bya4tyw8399/7bCqTnBYXy99mdeNkhMs3Q/0085bf4015673305fa011abb19a11e34/codeathon.png)](https://images.ctfassets.net/6bya4tyw8399/7bCqTnBYXy99mdeNkhMs3Q/0085bf4015673305fa011abb19a11e34/codeathon.png)

The repository contains 2 tools hacked during the last 3 days, the open-physiology-viewer and the sparc_converter

## Open-physiology-viewer

(from https://github.com/open-physiology/open-physiology-viewer)
Physiology deals with the body in terms of anatomical compartments that delineate portions of interest. The compartments can be defined at various anatomical scales, from organs to cells. Clinical and bioengineering experts are interested to see records of physical measurements associated with certain anatomical compartments.

ApiNATOMY is a methodology to coherently manage knowledge about the scale, parthood and connectivity of anatomical compartments as well as to represent and analyse process mechanisms and associated measurements. It consists of a knowledge model about biophysical entities, and a method to build knowledge representations of physiology processes in terms of biophysical entities and physical operations over these entities.
The current project visualizes 3d ApiNATOMY models as part of the NIH-SPARC MAP-CORE toolset. The main component in the current project accepts as input a JSON model and generates a force-directed graph layout satisfying relational constraints among model resources. The input model format is defined in the ApiNATOMY JSON Schema specification, check project documentation for more detail. Live demonstration of this application can be found here.

Build instructions
- Install Node.js.
- Clone (or download and unzip) the project to your file system: git clone https://github.com/metacell/open-physiology-viewer.git
- Go into the project directory: cd ./open-physiology-viewer
- Install build dependencies: npm install
- Run the build script: npm run build
- The compiled code is in the open-physiology/dist/ folder. After that you should be able to open a demo app test-app/index.html in your browser.

## SPARC Converter

The python tool is in charge of reading from the latest release from the SCKAN NIFSTD (NIF Standard Ontology), the generated neurons available in the sparc-nlp.ttl file, extract the relevant neuron families that can be connected to the WBKG housing lyphs and then generate an ApiNATOMY json model that will be opened with the open-physiology-viewer to highlight differences between the neuron families ingested.

The tool require a neo4j server, in charge of ingesting the ttl and output a graph representation of the same. In order to run such server:
- Install docker 
- run the script docker_setup.sh
- check the docker container log and wait for the server to start
- once done run the neuron_generator.py script

Note, the first time that the server is ran there are some extra settings to be performed in order for the tool to work properly (init neo4j graph and set constraint), the user will be prompted for such question, if the answer is not correct the tool might not work properly.

A version of the converter tool which includes information about species and sex for the converter neurons, is included in the species_and_sex folder of this repository. 

### Creating a model.

- In order to create a model, you first need to extract data from SPARC using the apinatomy-converter.
- To create a spreadsheet with models go to :
  ''' cd sparc_converter '''
- Run :
  ''' python neuron_generator.py model_name"
  Where model_name is 'mmset4', 'mmset3', 'prostate', 'semves' or 'mmset1', or other sparc model.
- Go to 
  ''' cd data/ '''
  And look for a spreasheet with same model name.
- You can use our deployment [apinatomy.dev.metacell.us](apinatomy.dev.metacell.us) and test the model by loading it. 
- To load it, launch [apinatomy.dev.metacell.us](apinatomy.dev.metacell.us) and click on the 'Load Model' icon. It's located on the left side bar, second from the right, looks like a folder icon.
- From File System, select the new created model spreasheet.
- Wait while it loads. 
- Toggle Settings panel on if not present, it's the Gears icon on the right sidebar.
- Go to Dynamic Groups, and click 'Enable Neuroview'
- Select of of the Dynamic groups at a time to visualize
