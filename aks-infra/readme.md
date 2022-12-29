start AKS cluster

# push image to github package
AzureAD+JayKim@LAB3-1228793957 MINGW64 ~/local/github/madforchili/jaykim-profile (main)
$ docker build -t jaykimprofile .

AzureAD+JayKim@LAB3-1228793957 MINGW64 ~/local/github/madforchili/jaykim-profile (main)
$ export CR_PAT=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

AzureAD+JayKim@LAB3-1228793957 MINGW64 ~/local/github/madforchili/jaykim-profile (main)
$ echo $CR_PAT | docker login ghcr.io -u madforchili --password-stdin
Login Succeeded

AzureAD+JayKim@LAB3-1228793957 MINGW64 ~/local/github/madforchili/jaykim-profile (main)
$ docker push ghcr.io/madforchili/jaykimprofile:latest
The push refers to repository [ghcr.io/madforchili/jaykimprofile]
a83da8676069: Pushed
0618d1e529fa: Pushed
6e96dd581d79: Pushed
acf5e0b2cf08: Pushed
d51445d70778: Pushed
b96b16a53835: Pushed
994393dc58e7: Pushed
latest: digest: sha256:d675f7669986cf7adcd0b858826db75981480f0729d0221a43ce3ef0207a9fb2 size: 1778

# for Azure VM deployment
update k8scp.sh find below code and update to canal.yaml

**kubectl apply -f https://projectcalico.docs.tigera.io/manifests/canal.yaml **


