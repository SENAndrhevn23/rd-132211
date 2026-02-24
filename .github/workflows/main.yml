plugins {
    java
    application
}

group = "net.minecraft"
version = "rd-132211"

repositories {
    mavenCentral()
}

java {
    sourceCompatibility = JavaVersion.VERSION_1_8
    targetCompatibility = JavaVersion.VERSION_1_8
}

/* =========================
   LWJGL NATIVES
   ========================= */

val natives: Configuration by configurations.creating {
    isTransitive = true
}

dependencies {
    implementation("org.lwjgl.lwjgl:lwjgl:2.9.3")
    implementation("org.lwjgl.lwjgl:lwjgl_util:2.9.3")

    natives("org.lwjgl.lwjgl:lwjgl-platform:2.9.3:natives-windows")
    natives("org.lwjgl.lwjgl:lwjgl-platform:2.9.3:natives-linux")
    natives("org.lwjgl.lwjgl:lwjgl-platform:2.9.3:natives-osx")
}

/* =========================
   APPLICATION ENTRY POINT
   ========================= */

application {
    mainClassName = "com.mojang.rubydung.RubyDung"
}

/* =========================
   CONFIGURE EXISTING RUN TASK
   ========================= */

tasks.named<JavaExec>("run") {
    dependsOn("extractNatives")
    workingDir = file("$projectDir/run")
    jvmArgs = listOf("-Dorg.lwjgl.librarypath=$projectDir/run/natives")
}

/* =========================
   EXTRACT NATIVES
   ========================= */

tasks.register<Copy>("extractNatives") {
    from(natives.map { zipTree(it) })
    into("$projectDir/run/natives")
}

/* =========================
   RUNNABLE JAR
   ========================= */

tasks.jar {
    manifest {
        attributes(
            "Main-Class" to "com.mojang.rubydung.RubyDung"
        )
    }
}
