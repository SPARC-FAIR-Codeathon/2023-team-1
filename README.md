
# Visualizing Neuronal Networks from SCKAN in the Open Physiology Viewer

[![N|Solid](https://images.ctfassets.net/6bya4tyw8399/7bCqTnBYXy99mdeNkhMs3Q/0085bf4015673305fa011abb19a11e34/codeathon.png)](https://images.ctfassets.net/6bya4tyw8399/7bCqTnBYXy99mdeNkhMs3Q/0085bf4015673305fa011abb19a11e34/codeathon.png)

The repository contains 2 tools hacked during the last 3 days, an updated version of the open-physiology-viewer and the sparc_converter

## Open-physiology-viewer

(from https://github.com/open-physiology/open-physiology-viewer)
Physiology deals with the body in terms of anatomical compartments that delineate portions of interest. The compartments can be defined at various anatomical scales, from organs down to tissues and cells.  It is particularly pertinent to the fields of Pharmacology, Cellular & Systems Biology, and Physiology to organize and model molecular data in its anatomical context, to compartmentalize biochemical and signal transduction processes into their subcellular compartments, meanwhile taking into account how molecules flow throughout these compartments to impact a biological system.

ApiNATOMY is a methodology to coherently manage knowledge about the scale, parthood and connectivity of anatomical compartments as well as to represent and analyse process mechanisms and associated measurements. It consists of a knowledge model about biophysical entities, and a method to build knowledge representations of physiology processes in terms of biophysical entities and physical operations over these entities.

The current project visualizes 3D ApiNATOMY models as part of the NIH-SPARC MAP-CORE toolset. The main component in the current project accepts as input a JSON model and generates a force-directed graph layout satisfying relational constraints among model resources. The input model format is defined in the ApiNATOMY JSON Schema specification, check project documentation for more detail. Live demonstration of this application can be found here.

Build instructions
- Install Node.js.
- Clone (or download and unzip) the project to your file system: git clone https://github.com/metacell/open-physiology-viewer.git
- Go into the project directory: cd ./open-physiology-viewer
- Install build dependencies: npm install
- Run the build script: npm run build
- The compiled code is in the open-physiology/dist/ folder. After that you should be able to open a demo app test-app/index.html in your browser.

## SPARC Converter

The Python tool is in charge of reading data from the latest release of the SCKAN NIFSTD (NIF Standard Ontology), which is the generated neurons available in the sparc-nlp.ttl file, extracting the relevant neuron families that can be connected to the Whole Body Knowledge Graph (WBKG, utilized as the database for the Open Physiology Viewer), and then generating an ApiNATOMY JSON model that will be opened with the open-physiology-viewer application for visualization and exploration.

The tool requires a neo4j server, in charge of ingesting the ttl and outputting a graph representation. In order to run the server:
- Install docker 
- Run the script docker_setup.sh
- Check the docker container log and wait for the server to start
- Once done run the neuron_generator.py script

Note, the first time that the server is run there are some extra settings the user will be prompted for in order for the tool to work properly (init neo4j graph and set constraints).

A version of the converter tool which extracts information from the turtle file concerning the species and sex of each SCKAN model is included in the species_and_sex folder of this repository.  This is intended to be utilized in the future (when the NIFSTD database has sufficiently grown) for comparing and contrasting the neuronal networks of different species or to analyze sexual dymorphisms.  The same approach can be used to make other comparisons, such as looking at differences in how a particular nerve passes through the left vs. right hemisphere of the body.

### Loading a model.

- In order to view a SCKAN model in ApiNATOMY, you first need to extract data from the SCKAN NIFSTD using the apinatomy-converter (see above).
- To create a spreadsheet with models go to :
  ''' cd sparc_converter '''
- Run :
  ''' python neuron_generator.py model_name"
  Where model_name is 'mmset4', 'mmset3', 'prostate', 'semves' or 'mmset1', or other SPARC model.
- Go to 
  ''' cd data/ '''
  And look for a spreasheet with same model name.
- Upload your spreadsheet model somewhere, here on github under data folder for example. Then you can use the URL where the model spreasheet was uploaded and pass it to as a query parameter to our deployment : [apinatomy.dev.metacell.us/?demoUrl=URL](apinatomy.dev.metacell.us).
  For example, we host our models on github by committing them to our repository. Then we use the raw Link address for the models and load them in apinatomy viewer. [https://apinatomy.dev.metacell.us/?demoUrl=https://raw.githubusercontent.com/open-physiology/open-physiology-viewer/feature/83_toggle/test/data/prostate.xlsx](https://apinatomy.dev.metacell.us/?demoUrl=https://raw.githubusercontent.com/open-physiology/open-physiology-viewer/feature/83_toggle/test/data/prostate.xlsx)
- You can use our deployment [apinatomy.dev.metacell.us](apinatomy.dev.metacell.us) and test the model by loading it. 
- To load it, launch [apinatomy.dev.metacell.us](apinatomy.dev.metacell.us) and click on the 'Load Model' icon. It's located on the left side bar, second from the top, and looks like a folder icon.
- From the File System, select the newly created model spreadsheet.
- Wait while it loads. 
- Toggle the Settings panel on if not present (it's the Gears icon on the right sidebar).
- Go to Dynamic Groups, and click 'Enable Neuroview'
- Select one of the Dynamic groups at a time to visualize the specific model of interest.
