# mgi-go-cams

## Model Generation Process

### Fetch current MGI data
```
wget http://www.informatics.jax.org/downloads/custom/go_cam_mgi.gpad -P source/
wget http://www.informatics.jax.org/downloads/custom/mgi.gpi -P source/
```
### Fetch current GO and RO JSON
```
wget http://current.geneontology.org/ontology/go.json
wget http://purl.obolibrary.org/obo/ro.owl
robot convert -i ro.owl -o ro.json
```
### Produce validated GPAD
```
ontobio-parse-assocs.py --file source/go_cam_mgi.gpad --format GPAD --gpi source/mgi.gpi -o products/go_cam_mgi_valid.gpad --report-md products/go_cam_mgi.report.md -r go.json -l "all" convert --to GPAD --format-version 2.0
```
### Generate GO-CAM TTL files
```
validate.py -v gpad2gocams --gpad_path products/go_cam_mgi_valid.gpad --gpi_path source/mgi.gpi --target models/ --ontology go.json --ontology ro.json --ttl -s production
```
## Dependencies
* `ontobio>=2.2.0`
* [ROBOT](http://robot.obolibrary.org/)
