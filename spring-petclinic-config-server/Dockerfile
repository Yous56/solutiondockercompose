FROM ubuntu
# Màj
RUN apt-get update -y
# installation wget
RUN apt-get install wget -y
#download java 17
RUN wget https://download.oracle.com/java/17/latest/jdk-17_linux-x64_bin.deb
RUN apt-get -qqy install openjdk-17-jdk openjdk-17-jre
# création de la variable d'env (SPRING_PROFILES_ACTIV) mais non utilisé => on peut la supp
ENV SPRING_PROFILES_ACTIVE=docker
# Récup d'un logocoel qui s'appelle (Dckersie) il permet au serices de s'attendre les uns les autres
# pour l'installer on définit une var d'env (DOCKERIZE_VERSION) et dans laquelle on met la valeur de 
# laversion
ENV DOCKERIZE_VERSION v0.7.0
# ici on update 
RUN apt-get update \
# ici on install wget ici on voit qu'il installé 2 fois => on peut en supprimer 
# une (car commandes en doblons)
    && apt-get install -y wget \
# installation du logocoel (dockersie) avaec la commande ci-dessous
    && wget -O dockerize.tar.gz https://github.com/jwilder/dockerize/releases/download/$DOCKERIZE_VERSION/dockerize-linux-amd64-$DOCKERIZE_VERSION.tar.gz \
# suppression des paquest qui ont servi à l'install et dont on n'a plus besoin
    && apt-get autoremove -yqq --purge wget && rm -rf /var/lib/apt/lists/*
# Désarchiver le fichier dockerise
RUN tar xzf dockerize.tar.gz
# on lui donne l'autorisation d'exécution
RUN chmod +x dockerize
# on copy config-servr.jar dans app.jar
COPY target/spring-petclinic-config-server-3.0.2.jar app.jar
# c'est le point d'entrée de l'application
ENTRYPOINT ["java", "-jar", "app.jar"]
