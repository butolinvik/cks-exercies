# Minimize base image footprint
# Secure your supply chain: whitelist allowed registries, sign and validate images
# Use static analysis of user workloads (e.g.Kubernetes resources, Docker files)
# Scan images for known vulnerabilities
#====================
docker run --name ubuntu -d ubuntu sh -c 'sleep 1d'