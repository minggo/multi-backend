```c++
struct BlendStateDescriptor
{
    bool blendEnabled;
    BlendFactor srcColorBlendFactor;
    BlendFactor dstColorBlendFactor;
    BlendFactor srcAlphaBlendFactor;
    BlendFactor dstAlphaBlendFactor;
    BlendOperation colorBlendOperation;
    BlendOerpation alphaBlendOperation;
};

struct StencilState
{
    CompareFunction stencilCompareFunction;
    StencilOperation stencilFailureOperation;
    StencilOperation depthFailureOperation;
    StencilOperation depthStencilPassOperation;
};

struct DepthStencilState
{
    CompareFunction depthCompareFunction;
    bool depthWriteEnabled;
    
    StencilState frontFaceStencil;
    StencilState backFaceStencil;
};

struct RasterizerState
{
    CullMode cullMode;
    TriangleFillMode fillMode;
    FrontFace frontFace;
    bool depthClipEnabled;
    bool scissorTestEnabled;
};

class ShaderModule
{
};

class VertexLayout
{
public:
    setAttribute(const std::string& name, VertexFormat format, uint32_t offset);
    setLayout(uint32_t stride, VertexStepMode stepMode);
};

class ResourceLayout
{
public:
    setResource(const std::string& name, ResourceKind kind, ShaderState state);    
};

class RenderPipelineDescriptor
{
public:
    void setBlendState(uint32_t slot, BlendState* blendState);
    void setDepthStencilState(const DepthStencilState& depthStencilState);
    void setRasterizerState(const RasterizerState& rasterizerState);
    void setPrimitiveTopology(PrimitiveTopology primitiveTopology);
    void setShaderModule(ShaderStage stage, ShaderModule* module);
    void setVertexLayout(const VertexLayout& vertexLayout);
    void setResourceLayout(const ResourceLayout& resourceLayout);
};

class RenderPipeline
{
    
};

struct TextureDescriptor
{
    uint32_t width;
    uint32_t height;
    uint32_t mipmapLevelCount;
    TextureFormat format;
    TextureDimension dimension; // 2d or cube
};

class Texture
{
public:
    update(uint8_t* data, uint32_t size);
};

struct BufferDescritpr
{
    uint8_t *data;
    uint32_t size;
    BufferUsage usage;
};

class RenderPassDescriptor
{
public:
    void setColorAttachment(uint32_t attachment, Texture* texture, LoadOp loadop);
    void setColorAttachmentClearColor(uint32_t attachment,
                                 float clearR,
                                 float clearG,
                                 float clearB,
                                 float clearA);
    void setDepthStencilAttachment(Texture* texture, LoadOp depthLoadOp, LoadOp stencilLoadOp);
    void setDepthStencilAttachmentClearValue(float clearDepth, uint32_t clearStencil);
};

class Device
{
public:
    RenderPipeline* createRenderPipeline(const RenderPipeLineDescriptor& descriptor);
    Texture* createTexture(const TextureDescriptor& descriptor);
    Buffer* createBuffer(const BufferDescriptor& descriptor);
    BlendState* createBlendState(const BlendStateDescriptor& descriptor);
    ShaderModule* createShaderModule(const std::string& source);
    CommandBuffer* createCommandBuffer();
    RenderPass* createRenderPass(const RenderPassDescriptor& descriptor);
};

class CommandBuffer
{
public:
    void beginRenderPass();
    void setRenderPipeline(RenderPipline* renderPipeline);
    void setRenderPass(RenderPass* renderPass);
    void setVertexBuffer(Buffer* buffer);
    void setIndexBuffer(Buffer* buffer);
    void setBlendColor(float r, float g, float b, float a);
    void setViewport(float x, float y, float w, float h);
    void setPushConstant(ShaderState stage, const std::string& name, const uint8_t* data, uint32_t size); // to set uniform
    void drawElements(uint32_t vertexCount);
    void drawIndexed(uint32_t indexCount);
    void endRenderPass();
};

```



