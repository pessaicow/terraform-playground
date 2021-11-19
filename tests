/* Local variables */
locals {
   tags = [
        "a:terraform",
        "bra.app:plataforma",
        "bra.depto:diti",
        "bra.empresa:bradesco",
        "bra.camada-cloud:paas",
        "bra.id:10545" //Conferir Tags
    ]
}
// CRIAÇÃO DO CONTAINER REGISTRY

data "ibm_resource_group" "group" {
    name = "all" //Definir resource group
}

resource "ibm_cr_namespace" "cr_namespace" {
    name = "test_tsoares" //Definir nome do namespace
    resource_group_id = data.ibm_resource_group.group.id
    tags = local.tags
}

resource "ibm_cr_retention_policy" "cr_retention_policy" {
    namespace = ibm_cr_namespace.cr_namespace.id
    images_per_repo = 10 //Definir Política de retenção de images no Registry
    retain_untagged = false //Permite manter images untagged no processamento de retention (false deleta untagged images)
}

/*

resource "ibm_iam_user_policy" "policy" {
    ibm_id = "tsoares@br.ibm.com" //Adicionar Manager role para o owner da Namespace (quem deve ser o owner?)
    roles  = ["Manager"]

    resources {
        service = "container-registry"
        resource = ibm_cr_namespace.cr_namespace.id
        resource_type = "namespace"
        region = var.region
    }
}

*/

// NECESSÁRIO - DEFINIR VPE PARA CONECTIVIDADE COM CONTAINER REGISTRY DOS VPCs
