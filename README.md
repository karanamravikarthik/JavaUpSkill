plugins {
    id 'org.springframework.boot' version '3.1.0'
    id 'io.spring.dependency-management' version '1.1.0'
    id 'java'
    id 'io.mateo.cxf-codegen' version '1.0.0' // CXF plugin for WSDL2Java
}

group = 'com.example'
version = '0.0.1-SNAPSHOT'
sourceCompatibility = '17'

repositories {
    mavenCentral()
}

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web-services'
    implementation 'javax.xml.bind:jaxb-api:2.3.1'
    testImplementation 'org.springframework.boot:spring-boot-starter-test'

    // Dependencies for CXF WSDL code generation
    cxfCodegen "jakarta.xml.ws:jakarta.xml.ws-api:2.3.3"
    cxfCodegen "jakarta.annotation:jakarta.annotation-api:1.3.5"
    compileOnly "jakarta.xml.ws:jakarta.xml.ws-api:2.3.3"
    compileOnly "jakarta.annotation:jakarta.annotation-api:1.3.5"
}

cxfCodegen {
    toolOptions {
        // Specify the WSDL file path
        wsdl.set(file("${projectDir}/src/main/resources/wsdl/example.wsdl"))
        suppressGeneratedDate.set(true) // Suppress the date annotation in generated files
        markGenerated.set(true)         // Mark generated files with annotations
        autoNameResolution.set(true)    // Automatically resolve name conflicts
        packageNames.set(["com.example.generated"]) // Specify the Java package for generated files
        outputDir.set(file("${buildDir}/generated-sources")) // Output directory for generated files
    }
}

tasks.named(JavaPlugin.COMPILE_JAVA_TASK_NAME) {
    dependsOn("wsdl2java") // Ensure WSDL generation happens before compilation
}

sourceSets {
    main {
        java {
            srcDir("${buildDir}/generated-sources") // Include generated sources in the classpath
        }
    }
}
