# Azure
<div align="center">
    <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/azure/azure-original.svg" width=100px/>
</div>

- [Azure](#azure)
  - [Azure Blob Storage com Java Spring Boot](#azure-blob-storage-com-java-spring-boot)
    - [Contextualizando](#contextualizando)
    - [Na prática com Spring boot](#na-prática-com-spring-boot)

## Azure Blob Storage com Java Spring Boot

O que você vai precisar:
- Token SAS
- URL
- Container criado

### Contextualizando

Azure Blob Storage
É uma solução de armazenamento oferecido pelo Azure e que possibilita o armazenamento de dados (imagens, documentos, videos etc).

O Azure Blob Storage é ideal para:

Fornecimento de dados diretamente no navegador;
Acesso distríbuido em arquivos;
Streaming de áudio e vídeo
Armazenamento de dados para backup, restauração ou arquivamento;
Armazenamento de logs de aplicação.
Os dados podem ser acessados via HTTP/HTTPS de qualquer lugar no mundo pois estão acessíveis por meio do Blob service REST API, do Azure PowerShell, da CLI do Azure ou através do uso de algum pacote oferecido pela Microsoft.

### Na prática com Spring boot
Abaixo verá um exemplo de um método para upload de arquivos

```java
@Override
    public String uploadFile(MultipartFile file) {
        String token = env.getProperty("azure_blob_token");
        String url = env.getProperty("azure_blob_url");
        String container = env.getProperty("azure_blob_container");

        String blobUrl = null;
        String blobName = file.getOriginalFilename();

        if (token != null && url != null) {
            BlobServiceClient blobServiceClient = new BlobServiceClientBuilder()
                    .endpoint(url)
                    .sasToken(token)
                    .buildClient();

            BlobContainerClient containerClient = blobServiceClient.getBlobContainerClient(container);
            BlobClient blobClient = containerClient.getBlobClient(blobName);

            BlobHttpHeaders blobHeaders = new BlobHttpHeaders().setContentType(file.getContentType());
            blobClient.setHttpHeaders(blobHeaders);

            try (InputStream inputStream = file.getInputStream()) {
                blobClient.upload(inputStream, file.getSize(), true);
                blobUrl = blobClient.getBlobUrl();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
        return blobUrl;
    }
```
