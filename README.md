# JavaUpSkill
JavaUpSkill

Here, I'll be measuring my progress!

Here, I'll be measuring my progress!
plugins {
    id 'java'
    id 'org.springframework.boot' version '3.3.5'
    id 'io.spring.dependency-management' version '1.1.6'
}

group = 'com.example.crs'
version = '0.0.1-SNAPSHOT'

java {
    toolchain {
        languageVersion = JavaLanguageVersion.of(17)
    }
}

repositories {
    maven { url nexusPublicRepoURL }
    maven { url nexusPublicRepoMavenCentralURL }
}

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web'
    testImplementation 'org.springframework.boot:spring-boot-starter-test'
    testRuntimeOnly 'org.junit.platform:junit-platform-launcher'

    // Swagger
    implementation 'org.springdoc:springdoc-openapi-starter-webmvc-ui:2.6.0'

    // Custom dependencies
    implementation 'com.discoverfinancial.ecc.servicelocator:ServiceLocator_WAS8_3.0.0_CM.9473'
    implementation 'com.discoverfinancial.ecc.dfscommon:DFSCommon:R8_DFSCommon_2.0.12_CM.526'

    implementation('ecc_util_pvob.utl_ecc_serviceinvocation_dist:serviceInvocation:R8_ServiceInvocation_1.7.1_CM') {
        exclude group: 'websphere8'
    }

    implementation 'ecc_ecm_pvob.utl_ecc_ecm_dist:ContentManagementServiceDelegate:R8_ContentMgmtService_3.0.18.9078_CM'
    implementation 'com.discover.mktgsvcs.secure:CRSClient:2.1.0'

    // JWT dependencies
    implementation 'com.discover.gateway:jwtApiAuthFilter:2.0.1'
    implementation 'com.dfs.spring.config:eastSpringUtil:1.0.4'

    // Explicitly include SLF4J and Logback
    implementation 'org.slf4j:slf4j-api:2.0.9'
    implementation 'ch.qos.logback:logback-classic:1.4.11'
}

configurations.all {
    exclude group: 'Log4j', module: 'Log4j'
    exclude group: 'org.slf4j', module: 'slf4j-log4j12'
    exclude group: 'commons-logging', module: 'commons-logging'
}
