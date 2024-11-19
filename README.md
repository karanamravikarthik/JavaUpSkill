dependencies {
    implementation platform('org.springframework.boot:spring-boot-dependencies:3.3.5') // Ensure Spring Boot manages versions
    implementation 'ch.qos.logback:logback-classic:1.4.11'
    implementation 'org.slf4j:slf4j-api:2.0.9'
}
implementation('com.discoverfinancial.ecc.serviceLocator:ServiceLocator_WAS8_3.0.0_CM.9473') {
    exclude group: 'ch.qos.logback'
    exclude group: 'org.slf4j'
}
