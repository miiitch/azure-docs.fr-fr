---
title: HDFS local bloqué en mode sans échec sur le cluster Azure HDInsight
description: Dépanner une instance locale d’Apache HDFS lorsqu’elle est bloquée en mode sans échec sur un cluster Apache dans Azure HDInsight
ms.service: hdinsight
ms.topic: troubleshooting
ms.date: 08/14/2019
ms.openlocfilehash: d34bf8d82aee14f5ba835f68a061555d24ee2621
ms.sourcegitcommit: 910a1a38711966cb171050db245fc3b22abc8c5f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/19/2021
ms.locfileid: "98944446"
---
# <a name="scenario-local-hdfs-stuck-in-safe-mode-on-azure-hdinsight-cluster"></a>Scénario : les HDFS locaux bloquent en mode sans échec sur le cluster Azure HDInsight

Cet article décrit les éventuelles solutions à appliquer pour résoudre les problèmes rencontrés lors d’interactions avec des clusters Azure HDInsight.

## <a name="issue"></a>Problème

Le stockage Apache HDFS (Hadoop Distributed File System) est bloqué en mode sans échec sur le cluster HDInsight. Vous recevez un message d’erreur semblable à ce qui suit :

```output
hdiuser@spark2:~$ hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
17/04/05 16:20:52 WARN retry.RetryInvocationHandler: Exception while invoking ClientNamenodeProtocolTranslatorPB.mkdirs over spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net/10.0.0.22:8020. Not retrying because try once and fail.
org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.hdfs.server.namenode.SafeModeException): Cannot create directory /temp. Name node is in safe mode.
It was turned on manually. Use "hdfs dfsadmin -safemode leave" to turn safe mode off.
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkNameNodeSafeMode(FSNamesystem.java:1359)
...
mkdir: Cannot create directory /temp. Name node is in safe mode.
```

## <a name="cause"></a>Cause

Le cluster HDInsight a été redimensionné avec très peu de nœuds, ou le nombre de nœuds est proche du facteur de réplication HDFS.

## <a name="resolution"></a>Résolution

1. Créez un rapport sur l’état du stockage HDFS du cluster HDInsight à l’aide des commandes suivantes :

    ```bash
    hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
    ```

1. Vérifiez l’intégrité du stockage HDFS du cluster HDInsight à l’aide des commandes suivantes :

    ```bash
    hdiuser@spark2:~$ hdfs fsck -D "fs.default.name=hdfs://mycluster/" /
    ```

1. Si aucun bloc n’est manquant, endommagé ou sous-répliqué ou si ces blocs peuvent être ignorés, exécutez la commande suivante pour désactiver le mode sans échec sur le nœud de nom :

    ```bash
    hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
    ```

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [troubleshooting next steps](../../../includes/hdinsight-troubleshooting-next-steps.md)]