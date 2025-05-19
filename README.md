# hello-world
hello-world
world
   world




<bean id="multiResourceItemReader" class="org.springframework.batch.item.file.MultiResourceItemReader">
    <property name="resources" ref="sortedResources"/>
    <property name="delegate" ref="jsonItemReader"/>
</bean>

<bean id="sortedResources" factory-method="getSortedResources" class="com.example.ResourceFactory"/>


public class ResourceFactory {
    public Resource[] getSortedResources() {
        File folder = new File("/path/to/json/files");
        File[] files = folder.listFiles((dir, name) -> name.endsWith(".json"));

        if (files == null) return new Resource[0];

        Arrays.sort(files, Comparator.comparingLong(File::lastModified));

        return Arrays.stream(files)
                     .map(FileSystemResource::new)
                     .toArray(Resource[]::new);
    }
}
