# Publishing Guide for Oxide VS Code Theme

This guide will walk you through publishing the Oxide theme to the VS Code Marketplace.

## Prerequisites Checklist

✅ All metadata files created:
- `package.json` - Complete with publisher, repository, keywords
- `README.md` - Template-based documentation
- `LICENSE` - MIT License
- `CHANGELOG.md` - Version history
- `.vscodeignore` - Package exclusion rules
- `assets/logo.png` - Extension icon (128x128px)
- `assets/preview.png` - Theme preview screenshot

## Step 1: Install Publishing Tools

```bash
# Install vsce (VS Code Extension CLI)
npm install -g @vscode/vsce
```

## Step 2: Create Azure DevOps Account

1. Go to https://dev.azure.com
2. Sign in with your Microsoft account (or create one)
3. Click "Create organization" if you don't have one
4. Follow the setup wizard

## Step 3: Generate Personal Access Token (PAT)

1. Go to https://dev.azure.com
2. Click on your profile icon (top right) → **Personal access tokens**
3. Click **+ New Token**
4. Configure token:
   - **Name**: "VS Code Marketplace Publishing" (or any name)
   - **Organization**: Select **All accessible organizations** ⚠️ IMPORTANT
   - **Expiration**: Set your preferred expiration (recommend 90 days or 1 year)
   - **Scopes**: Click **Custom defined**
   - Scroll down to **Marketplace** section
   - Check **Manage** ✅
5. Click **Create**
6. **COPY THE TOKEN IMMEDIATELY** - you won't see it again!
   - Save it somewhere secure (like a password manager)

## Step 4: Create Publisher Account

1. Go to https://marketplace.visualstudio.com/manage
2. Sign in with the same Microsoft account from Step 2
3. Click **Create publisher**
4. Fill in the form:
   - **ID**: `oxidescheme` ⚠️ CANNOT BE CHANGED LATER
   - **Name**: `Oxide Theme` (or "oxidescheme")
   - **Email**: Your contact email
   - **Logo**: Optional (can add later)
   - **Website**: `https://github.com/oxidescheme`
5. Click **Create**

## Step 5: Verify Publisher with vsce

```bash
# Navigate to your extension directory
cd /Users/jakubmazur/git/oxide/vscode

# Login to vsce
vsce login oxidescheme

# When prompted, paste your Personal Access Token
# It will verify the connection
```

Expected output:
```
https://marketplace.visualstudio.com/manage/publishers/
Personal Access Token for publisher 'oxidescheme': ****************************************************

The Personal Access Token verification succeeded for the publisher 'oxidescheme'.
```

## Step 6: Test Package Locally (Optional but Recommended)

```bash
# Package the extension (creates .vsix file)
vsce package

# This will create: oxide-theme-0.1.0.vsix
```

Test the packaged extension:
1. Open VS Code
2. Go to Extensions view
3. Click "..." menu → "Install from VSIX..."
4. Select `oxide-theme-0.1.0.vsix`
5. Test the theme thoroughly

## Step 7: Publish to Marketplace

### Option A: Direct Publishing (Recommended)

```bash
# Publish directly
vsce publish

# Or publish with specific version bump
# vsce publish patch  # 0.1.0 → 0.1.1
# vsce publish minor  # 0.1.0 → 0.2.0
# vsce publish major  # 0.1.0 → 1.0.0
```

### Option B: Manual Upload

1. Package first: `vsce package`
2. Go to https://marketplace.visualstudio.com/manage/publishers/oxidescheme
3. Click **+ New extension** → **Visual Studio Code**
4. Upload the `.vsix` file
5. Click **Upload**

## Step 8: Verify Publication

1. Go to https://marketplace.visualstudio.com/items?itemName=oxidescheme.oxide-theme
2. Verify all information displays correctly:
   - Icon
   - Screenshots
   - Description
   - Installation instructions
3. Try installing from marketplace in VS Code:
   ```
   code --install-extension oxidescheme.oxide-theme
   ```

## Common Issues & Solutions

### Issue: "403 Forbidden" or "401 Unauthorized"

**Solution**: 
- Check that PAT was created with "All accessible organizations"
- Verify PAT has "Marketplace (Manage)" scope
- Try regenerating the PAT

### Issue: "Publisher not found"

**Solution**:
- Verify publisher ID matches exactly: `oxidescheme`
- Check you're logged into the correct Microsoft account

### Issue: "Extension already exists"

**Solution**:
- Extension name must be unique across the entire marketplace
- If `oxide-theme` is taken, try `oxide-vscode-theme` or similar

### Issue: "SVG images not allowed"

**Solution**:
- Ensure icon is PNG format (not SVG)
- Check that no SVGs are referenced in README

## Updating the Extension

For future updates:

```bash
# Update version in package.json or use vsce
vsce publish patch  # or minor/major

# This will:
# 1. Update version in package.json
# 2. Create git tag
# 3. Publish to marketplace
```

Remember to update CHANGELOG.md with each release!

## Monitoring & Analytics

View extension statistics:
1. Go to https://marketplace.visualstudio.com/manage
2. Select your extension
3. View "Acquisition Trend" and "Ratings & Reviews"

## Next Steps After Publishing

1. **GitHub Release**: Create a GitHub release with the .vsix file
2. **Announcement**: Share on social media, Discord, etc.
3. **Documentation**: Link to marketplace from main oxide repository
4. **Monitor**: Watch for issues and user feedback

## Resources

- [VS Code Publishing Guide](https://code.visualstudio.com/api/working-with-extensions/publishing-extension)
- [Extension Manifest Reference](https://code.visualstudio.com/api/references/extension-manifest)
- [Marketplace Management](https://marketplace.visualstudio.com/manage)

---

**Ready to publish?** Follow the steps above and your Oxide theme will be live on the VS Code Marketplace! 🎉
