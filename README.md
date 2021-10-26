```glsl
#version 330 core

struct Material {
  sampler2D diffuse;
  vec3      specular;
};

uniform Material material;

out vec4 FragColor;

void main() {
  vec3 color = material.specular * texture(material.diffuse, vec2(0, 0)).rgb;
  FragColor = vec4(color, 1);
}
```
```
; SPIR-V
; Version: 1.0
; Generator: Khronos Glslang Reference Front End; 10
; Bound: 39
; Schema: 0
               OpCapability Shader
          %1 = OpExtInstImport "GLSL.std.450"
               OpMemoryModel Logical GLSL450
               OpEntryPoint Fragment %main "main" %FragColor
               OpExecutionMode %main OriginLowerLeft
               OpSource GLSL 330
               OpName %main "main"
               OpName %color "color"
               OpName %Material "Material"
               OpMemberName %Material 0 "diffuse"
               OpMemberName %Material 1 "specular"
               OpName %material "material"
               OpName %FragColor "FragColor"
               OpDecorate %material Location 0
               OpDecorate %material DescriptorSet 0
               OpDecorate %FragColor Location 0
       %void = OpTypeVoid
          %3 = OpTypeFunction %void
      %float = OpTypeFloat 32
    %v3float = OpTypeVector %float 3
%_ptr_Function_v3float = OpTypePointer Function %v3float
         %10 = OpTypeImage %float 2D 0 0 0 1 Unknown
         %11 = OpTypeSampledImage %10
   %Material = OpTypeStruct %11 %v3float
%_ptr_UniformConstant_Material = OpTypePointer UniformConstant %Material
   %material = OpVariable %_ptr_UniformConstant_Material UniformConstant
        %int = OpTypeInt 32 1
      %int_1 = OpConstant %int 1
%_ptr_UniformConstant_v3float = OpTypePointer UniformConstant %v3float
      %int_0 = OpConstant %int 0
%_ptr_UniformConstant_11 = OpTypePointer UniformConstant %11
    %v2float = OpTypeVector %float 2
    %float_0 = OpConstant %float 0
         %26 = OpConstantComposite %v2float %float_0 %float_0
    %v4float = OpTypeVector %float 4
%_ptr_Output_v4float = OpTypePointer Output %v4float
  %FragColor = OpVariable %_ptr_Output_v4float Output
    %float_1 = OpConstant %float 1
       %main = OpFunction %void None %3
          %5 = OpLabel
      %color = OpVariable %_ptr_Function_v3float Function
         %18 = OpAccessChain %_ptr_UniformConstant_v3float %material %int_1
         %19 = OpLoad %v3float %18
         %22 = OpAccessChain %_ptr_UniformConstant_11 %material %int_0
         %23 = OpLoad %11 %22
         %28 = OpImageSampleImplicitLod %v4float %23 %26
         %29 = OpVectorShuffle %v3float %28 %28 0 1 2
         %30 = OpFMul %v3float %19 %29
               OpStore %color %30
         %33 = OpLoad %v3float %color
         %35 = OpCompositeExtract %float %33 0
         %36 = OpCompositeExtract %float %33 1
         %37 = OpCompositeExtract %float %33 2
         %38 = OpCompositeConstruct %v4float %35 %36 %37 %float_1
               OpStore %FragColor %38
               OpReturn
               OpFunctionEnd
```
