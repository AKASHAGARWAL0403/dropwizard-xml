# Dropwizard XML Bundle
[Dropwizard](https://github.com/dropwizard/dropwizard) extension for high performance processing and validation of XML.

Uses:
* [Jackson XML Provider](https://github.com/FasterXML/jackson-jaxrs-xml-provider) Jackson XML Provider with woodstox under the hood.
* [Hibernate Validator](http://hibernate.org/validator/) same Dropwizard validation behvaiour for XML 

## Status

<a href='https://bintray.com/yunspace/dropwizard/dropwizard-xml/view?source=watch' alt='Get automatic notifications about new "dropwizard-xml" versions'><img src='https://www.bintray.com/docs/images/bintray_badge_color.png'></a>
[![Download](https://api.bintray.com/packages/yunspace/dropwizard/dropwizard-xml/images/download.svg)](https://bintray.com/yunspace/dropwizard/dropwizard-xml/_latestVersion)

## Dependencies
This project is pegged against Dropwizard's release number and try to use the same Jackson dependency to avoid conflicts.

| Dropwizard-XML   | Dropwizard     | Jackson   | Woodstox | Stax  |
| ---------------- | -------------- | --------- | -------- |------ |
| 0.7.1-2          | 0.7.1          | 2.3.3     | 4.4.1    | 3.1.4 |
| 0.8.0-1-SNAPSHOT | 0.8.0-SNAPSHOT | 2.4.1     | 4.4.1    | 3.1.4 |

## Usage
Dropwizard XML Provider is hosted by [JCenter](https://bintray.com/bintray/jcenter).

You can add the dependency to your project by Maven:

    <repositories>
        <repository>
            <id>jcenter</id>
            <url>http://jcenter.bintray.com</url>
        </repository>
    </repositories>
    <dependency>
        <groupId>com.yunspace.dropwizard</groupId>
        <artifactId>dropwizard-xml</artifactId>
        <version>0.7.1-2</version>
        <scope>compile</scope>
    </dependency>

Or Gradle:

    repositories {
        jcenter()
        mavenCentral()
    }
    dependencies {
        compile 'com.yunspace.dropwizard:dropwizard-xml:0.7.1-2
    }
    
Add the XMLBundle

    bootstrap.addBundle(new XmlBundle());

Annotate your Resources:

    @Produces(MediaType.APPLICATION_XML) @Consumes(MediaType.APPLICATION_XML)

Annotate your model POJO with jackson-dataformat-xml bindings:

    @JacksonXmlRootElement @JacksonXmlProperty @JacksonXmlElementWrapper @JacksonXmlText

Use validation/ignore annotations as you would normally:

    @NotNull @Min @JsonIgnore

## Advanced Usage

You can further custom the behaviour of your XML Mapper by passing in a JacksonXmlModule:

    bootstrap.addBundle(new XmlBundle(jacksonXmlModule));

Or enable various serialisation/deserialisation features

    XmlBundle indentXmlBundle = new XmlBundle();
    indentXmlBundle.getXmlMapper().enable(SerializationFeature.INDENT_OUTPUT);
    bootstrap.addBundle(indentXmlBundle);

##Sample project
See dropwizard-xml-example subproject.
