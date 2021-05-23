## Example Operator built from Operator SDK

Docker Image Location quay.io/itroyano/example-operator
OLM Bundle Image Location quay.io/itroyano/example-operator-bundle
Reference https://sdk.operatorframework.io/docs/building-operators/golang/tutorial/

### Commands List

mkdir -p $HOME/projects/example-operator
cd projects/example-operator
operator-sdk init --domain example.com --repo github.com/itroyano/example-operator --skip-go-version-check
operator-sdk create api --group example.com --version v1alpha1 --kind Examplecr --resource --controller

DO CHANGES

make generate
make manifests
make docker-build docker-push

DO OLM CHANGES

make bundle
make bundle-build bundle-push

### Running Locally

kind create cluster
operator-sdk olm install
operator-sdk run bundle quay.io/itroyano/example-operator-bundle:v0.0.1
kubectl create -f config/samples/examples_v1alpha1_examplecr.yaml
