/*
  Supabase SQL Function: enrich_lead

  Purpose:
  - Safely enrich creator records without overwriting existing data
  - Updates only NULL fields using COALESCE
  - Matches rows by (creator_handle, platform)

  How to use:
  1. Open Supabase Dashboard → SQL Editor
  2. Paste this file
  3. Click Run
*/

CREATE OR REPLACE FUNCTION public.enrich_lead(
  p_creator_handle TEXT,
  p_platform TEXT,
  p_payload JSONB
)
RETURNS VOID
LANGUAGE plpgsql
AS $$
BEGIN
  UPDATE public.Leads3
  SET
    userid                = COALESCE(p_payload->>'userid', userid),
    username              = COALESCE(p_payload->>'username', username),
    full_name             = COALESCE(p_payload->>'full_name', full_name),
    biography             = COALESCE(p_payload->>'biography', biography),
    category              = COALESCE(p_payload->>'category', category),
    profile_picture       = COALESCE(p_payload->>'profile_picture', profile_picture),
    profile_picture_hd    = COALESCE(p_payload->>'profile_picture_hd', profile_picture_hd),

    exists                = COALESCE((p_payload->>'exists')::BOOLEAN, exists),
    has_profile_pic       = COALESCE((p_payload->>'has_profile_pic')::BOOLEAN, has_profile_pic),
    is_private            = COALESCE((p_payload->>'is_private')::BOOLEAN, is_private),
    is_business_account   = COALESCE((p_payload->>'is_business_account')::BOOLEAN, is_business_account),
    is_verified            = COALESCE((p_payload->>'is_verified')::BOOLEAN, is_verified),
    video_content_creator = COALESCE((p_payload->>'video_content_creator')::BOOLEAN, video_content_creator),
    uses_link_in_bio      = COALESCE((p_payload->>'uses_link_in_bio')::BOOLEAN, uses_link_in_bio),

    follower_count        = COALESCE((p_payload->>'follower_count')::BIGINT, follower_count),
    following_count       = COALESCE((p_payload->>'following_count')::BIGINT, following_count),
    media_count           = COALESCE((p_payload->>'media_count')::BIGINT, media_count),

    links_in_bio          = COALESCE(p_payload->'links_in_bio', links_in_bio),
    post_data             = COALESCE(p_payload->'post_data', post_data),

    avg_likes             = COALESCE((p_payload->>'avg_likes')::NUMERIC, avg_likes),
    avg_comments          = COALESCE((p_payload->>'avg_comments')::NUMERIC, avg_comments),
    total_posts_analyzed  = COALESCE((p_payload->>'total_posts_analyzed')::INTEGER, total_posts_analyzed),
    engagement_rate       = COALESCE((p_payload->>'engagement_rate')::NUMERIC, engagement_rate),

    raw_response          = COALESCE(p_payload->'raw_response', raw_response),
    enriched_at           = COALESCE((p_payload->>'enriched_at')::TIMESTAMPTZ, enriched_at),
    credits_cost          = COALESCE(p_payload->>'credits_cost', credits_cost)

  WHERE creator_handle = p_creator_handle
    AND platform = p_platform;
END;
$$;
